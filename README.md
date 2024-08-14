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
            
            
            sqlite_file_name = "database.db"
            sqlite_url = f"sqlite:///{sqlite_file_name}"
            
            connect_args = {"check_same_thread": False}
            engine = create_engine(sqlite_url, echo=True, connect_args=connect_args)
            
            
            def create_db_and_tables():
                SQLModel.metadata.create_all(engine)
            
            
            app = FastAPI()
            
            
            @app.on_event("startup")
            def on_startup():
                create_db_and_tables()
            
            
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
                    

  * Remove following lines

            sqlite_file_name = "database.db"

 

