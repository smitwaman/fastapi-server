Write main.py for "hello-world" file and requirements.txt

from fastapi import FastAPI

# Create an instance of FastAPI
app = FastAPI()

# Define a route with GET method
@app.get("/")
def read_root():
    return {"message": "Hello, World!"}
