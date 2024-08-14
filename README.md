# sqlmodel.

@ https://www.youtube.com/watch?v=m2rm94oUTkg&list=PLplW4d4HPsELkAU4_Iofhus90wRwRNe1o

## make folder with app within CURD 

      Poetry new CURD --name app

## change folder to CURD

      cd CURD 

## open CURD folder in VS 

      code .

## install dependencies
* you can give search in neon documents sqlalchmay for getting psycopg2-bianry

        poetry add fastapi sqlmodel psycopg2-binary uvicorn[standard]    

## Now search "FastAPI and Pydantic - Intro" in Sql documentation
* No go to "Simple Hero API with FastAPI"

            from fastapi import FastAPI
from sqlmodel import Field, Session, SQLModel, create_engine, select

* copy full code for api and paste in main.py file

            class Hero(SQLModel, table=True):
                id: int | None = Field(default=None, primary_key=True)
                name: str = Field(index=True)
                secret_name: str
                age: int | None = Field(default=None, index=True)
            
            
            # sqlite_file_name = "database.db" # delete it 
            # sqlite_url = f"sqlite:///{sqlite_file_name}" # change it to below line variable name and copy from neon data base and paste in f"  "
            DATABASE_URL = F"postgresql://neondb_owner:E5act1oUAlxd@ep-rapid-bush-a5h1k4yn.us-east-2.aws.neon.tech/hero?sslmode=require"
            
            # connect_args = {"check_same_thread": False} # delete it
            # engine = create_engine(sqlite_url, echo=True, connect_args=connect_args)
            engine = create_engine(DATABASE_URL)
            
            
            def create_db_and_tables():
                SQLModel.metadata.create_all(engine)
            
            
            app = FastAPI()
            
            
            #@app.on_event("startup") # replace this whole block with lifespan
            #def on_startup():
            #    create_db_and_tables()
            
            
            @app.post("/heroes/")
            def create_hero(hero: Hero):
                with Session(engine) as session:
                    session.add(hero)
                    session.commit()
                    session.refresh(hero)
                    return hero
            
            
            @app.get("/heroes/")
            def read_heroes():
                with Session(engine) as session:
                    heroes = session.exec(select(Hero)).all()
                    return heroes
                    


