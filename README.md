# Fast-API

## This project is deployed on render and access via online through this link  -  https://fast-api-36yt.onrender.com


from os import name
from fastapi import FastAPI
from pydantic import BaseModel
from typing import List

class Student(BaseModel):
    name: str
    email : str
    age : int
    Roll_no : int
    Department : str

class StudentResponse(BaseModel):
    name: str
    email : str
    age : int
    Roll_no : int
    Department : str



app = FastAPI()

@app.get("/")
def read_root():
    return {"HELLO":"SANJAY"}   

# Create a student
@app.post("/students", response_model=StudentResponse)
def create_student(student: Student):
    students_db.append(student)
    return student


# Get all students
@app.get("/students", response_model=List[StudentResponse])
def get_all_students():
    return students_db


# Get student by roll number
@app.get("/students/{roll_no}", response_model=StudentResponse)
def get_student(roll_no: int):
    for student in students_db:
        if student.Roll_no == roll_no:
            return student
    return {"error": "Student not found"}

@app.put("/students/{roll_no}", response_model=StudentResponse)
def get_student(roll_no: int):
    for student in students_db:
        if student.Roll_no == roll_no:
            return student
    return {"error": "Student not found"}
