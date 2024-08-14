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
* copy full code for api and paste in main.py file
* Remove following lines
*        sqlite_file_name = "database.db"
