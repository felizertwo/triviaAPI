# Trivia API Project

  

------------


This project is a game where the users can answer questions to check their knowledge in specific topics. Todos for the project were to create an API and test development as followed.


All backend code follows [PEP8 style guidelines](https://www.python.org/dev/peps/pep-0008/).

  

## Getting Started

  

------------

### **Pre-requisites and Local Development**

  

Developers using this project should already have Postgres (psql), python3, pip, node and npm or yarn on their local machines.

  

**Frontend**

  

From the frontend folder run **npm install** or **yarn**. All node_modules will be installed.

To run the Frontend Application run the following command.

  

**npm start **or **yarn start**

  

These command will start the client.

By default, the frontend will run on http://127.0.0.1:3000

  

**Backend**

  

From the backend folder run **pip install -r requirements.txt** . All required packages are included in the requirements file.

  
First you need to initiate the database with the following commands:


```
psql postgres < setup.sql
psql trivia < trivia.psql
```


To run the backend application run the following commands:

  
```
export FLASK_APP=flaskr

export FLASK_ENV=development

flask run
```

  

The commands put the application in development and directs our application to use the __init__.py file in our flaskr folder. Working in development shows an interactive devugger in the console and restarts the server whenever changes are made.


  

If you run the application on windows, look for the commands in the [Flask documentation](http://flask.pocoo.org/docs/1.0/tutorial/factory/)

****

The backend application is running on http://127.0.0.1:5000/ by default and is a proxy in the frontend configuration.

  

### Testing

  

In order to run the tests navigate to the backend folder and run the following commands:

(Assuming you have already initated the database as described in the backend part)

```


dropdb trivia_test

createdb trivia_test

psql trivia_test < trivia.psql

python test_flaskr.py
```

  

The first time you run the tests, omit the dropdb command.

  

All tests are kept in that file and should be maintained as updates are made to app functionality.

  

### API Reference

  

------------

  

**Getting Started**

  

- Base URL: At present this application is only hosted locally and is not hosted as a baseURL.

- The backend is hosted by default at http://127.0.0.1:5000/ , which is set as a proxy in the frontend configuration.

- Authentication: This version does not require authentication or API keys.

  

### Error Handling


Errors are returned as JSON in the following format:<br>

    {
        "success": False,
        "error": 404,
        "message": "resource not found"
    }

  

The API will return three types of errors:

  

400 – bad request

404 – resource not found

422 – unprocessable

  

### Endpoints

  

**GET /categories**

  

- General: Returns a list categories.

  

* Sample: `curl http://127.0.0.1:5000/categories`<br>

        {
            "categories": {
                "1": "Science", 
                "2": "Art", 
                "3": "Geography", 
                "4": "History", 
                "5": "Entertainment", 
                "6": "Sports"
            }, 
            "success": true
        }

**GET /questions**

  

- General

- - Returns a list questions.

- - Results are paginated by 10 entries per page.

- - Returns list of categories and total number of questions

  

* Sample: `curl http://127.0.0.1:5000/questions`<br>

        {
            "categories": {
                "1": "Science", 
                "2": "Art", 
                "3": "Geography", 
                "4": "History", 
                "5": "Entertainment", 
                "6": "Sports"
            }, 
            "questions": [
                {
                    "answer": "Colorado, New Mexico, Arizona, Utah", 
                    "category": 3, 
                    "difficulty": 3, 
                    "id": 164, 
                    "question": "Which four states make up the 4 Corners region of the US?"
                }, 
                {
                    "answer": "Muhammad Ali", 
                    "category": 4, 
                    "difficulty": 1, 
                    "id": 9, 
                    "question": "What boxer's original name is Cassius Clay?"
                }, 
                {
                    "answer": "Apollo 13", 
                    "category": 5, 
                    "difficulty": 4, 
                    "id": 2, 
                    "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
                }, 
                {
                    "answer": "Tom Cruise", 
                    "category": 5, 
                    "difficulty": 4, 
                    "id": 4, 
                    "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
                }, 
                {
                    "answer": "Edward Scissorhands", 
                    "category": 5, 
                    "difficulty": 3, 
                    "id": 6, 
                    "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
                }, 
                {
                    "answer": "Brazil", 
                    "category": 6, 
                    "difficulty": 3, 
                    "id": 10, 
                    "question": "Which is the only team to play in every soccer World Cup tournament?"
                }, 
                {
                    "answer": "Uruguay", 
                    "category": 6, 
                    "difficulty": 4, 
                    "id": 11, 
                    "question": "Which country won the first ever soccer World Cup in 1930?"
                }, 
                {
                    "answer": "George Washington Carver", 
                    "category": 4, 
                    "difficulty": 2, 
                    "id": 12, 
                    "question": "Who invented Peanut Butter?"
                }, 
                {
                    "answer": "Lake Victoria", 
                    "category": 3, 
                    "difficulty": 2, 
                    "id": 13, 
                    "question": "What is the largest lake in Africa?"
                }, 
                {
                    "answer": "The Palace of Versailles", 
                    "category": 3, 
                    "difficulty": 3, 
                    "id": 14, 
                    "question": "In which royal palace would you find the Hall of Mirrors?"
                }
            ], 
            "success": true, 
            "total_questions": 19
        }
  
**DELETE /questions/<int:id>**

- General

- - Deletes a question by id using url parameters.

- - Returns id of deleted question upon success.

* Sample: `curl http://127.0.0.1:5000/questions/6 -X DELETE`<br>

        {
            "deleted": 6, 
            "success": true
        }


**POST /questions**

  

This endpoint either creates a new question or returns search results.

  

1. If no search term is included in request:

  

- General:

- - Creates a new question using JSON request parameters.

- - Returns JSON object with newly created question.

  

Sample: `curl http://127.0.0.1:5000/questions -X POST -H "Content-Type: application/json" -d '{
            "question": "Which US state contains an area known as the Upper Penninsula?",
            "answer": "Michigan",
            "difficulty": 3,
            "category": "3"
        }'`

        {
            "created": 25,
            "success": True,
        }

  

2. If search term is included in request:

- General:

- - Searches for questions using search term in JSON request parameters.

- - Returns JSON object with paginated matching questions.

* Sample: `curl http://127.0.0.1:5000/questions -X POST -H "Content-Type: application/json" -d '{"searchTerm": "which"}'`<br>

        {
            "questions": [
                {
                    "answer": "Brazil", 
                    "category": 6, 
                    "difficulty": 3, 
                    "id": 10, 
                    "question": "Which is the only team to play in every soccer World Cup tournament?"
                }, 
                {
                    "answer": "Uruguay", 
                    "category": 6, 
                    "difficulty": 4, 
                    "id": 11, 
                    "question": "Which country won the first ever soccer World Cup in 1930?"
                }, 
                {
                    "answer": "The Palace of Versailles", 
                    "category": 3, 
                    "difficulty": 3, 
                    "id": 14, 
                    "question": "In which royal palace would you find the Hall of Mirrors?"
                }, 
                {
                    "answer": "Agra", 
                    "category": 3, 
                    "difficulty": 2, 
                    "id": 15, 
                    "question": "The Taj Mahal is located in which Indian city?"
                }, 
                {
                    "answer": "Escher", 
                    "category": 2, 
                    "difficulty": 1, 
                    "id": 16, 
                    "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
                }, 
                {
                    "answer": "Jackson Pollock", 
                    "category": 2, 
                    "difficulty": 2, 
                    "id": 19, 
                    "question": "Which American artist was a pioneer of Abstract Expressionism, and a leading exponent of action painting?"
                }, 
                {
                    "answer": "Scarab", 
                    "category": 4, 
                    "difficulty": 4, 
                    "id": 23, 
                    "question": "Which dung beetle was worshipped by the ancient Egyptians?"
                }, 
                {
                    "answer": "Michigan", 
                    "category": 3, 
                    "difficulty": 3, 
                    "id": 173, 
                    "question": "Which US state contains an area known as the Upper Penninsula?"
                }
            ], 
            "success": true, 
            "total_questions": 18
        }


**GET /categories/<int:id>/questions**

  

- General:

- - Gets questions by category id using url parameters.

- - Returns JSON object with paginated matching questions.

  * Sample: `curl http://127.0.0.1:5000/categories/1/questions`<br>

        {
            "current_category": "Science", 
            "questions": [
                {
                    "answer": "The Liver", 
                    "category": 1, 
                    "difficulty": 4, 
                    "id": 20, 
                    "question": "What is the heaviest organ in the human body?"
                }, 
                {
                    "answer": "Alexander Fleming", 
                    "category": 1, 
                    "difficulty": 3, 
                    "id": 21, 
                    "question": "Who discovered penicillin?"
                }, 
                {
                    "answer": "Blood", 
                    "category": 1, 
                    "difficulty": 4, 
                    "id": 22, 
                    "question": "Hematology is a branch of medicine involving the study of what?"
                }
            ], 
            "success": true, 
            "total_questions": 18
        }


**POST /quizzes**

  

- General:

- - Allows users to play the quiz game.

- - Uses JSON request parameters of category and previous questions.

- - Returns JSON object with random question not among previous questions.

* Sample: `curl http://127.0.0.1:5000/quizzes -X POST -H "Content-Type: application/json" -d '{"previous_questions": [20, 21], "quiz_category": {"type": "Science", "id": "1"}}'`

        <br>

        {
            "question": {
                "answer": "Blood", 
                "category": 1, 
                "difficulty": 4, 
                "id": 22, 
                "question": "Hematology is a branch of medicine involving the study of what?"
            }, 
            "success": true
        }

  

### **Authors**

Felix Eigenbrodt authored the Backend Application, included the test file and README.md.

All the other project files (model.py and frontend) were created by Udacity as a project template for the Full Stack Web Developer Nanodegree.
