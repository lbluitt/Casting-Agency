# Full Stack Nanodegree Final Project

## Udacity Casting Agency 

This project is aimed to demonstrate the knowledge acquired througout all the courses of Udacity's Full Stack Nanodegree, combining and not limited to showcase concepts about python, testing (unit tests), relational databases, authentication (using JWT), Role Based Access Control (RBAC) and deployment. 

To bring up a hands-on project that can illustrate concepts learned, this project consists on an application - a casting agency - that is capable of managing Actors and Movies. This application allows you to:

1. Get movies and actors
2. Add movies and actors
3. Remove movies and actors
4. Patch movies and actors

Also, authentication and RBAC is required in order to make use of this application. For this first iteration on the implementation of this project, the project is available through a Backend API.

### Authentication
This leverages authentication to **Auth0** [https://auth0.com/]. Roles and permissions are needed to make use of the app. The setup.sh file inclues pre-generated token for each available role to test the app.

## Roles
# Casting Assistant
- Can get actors and movies

# Casting Director
- Can to perform all operations that the casting assistant has
- Able to modify actors and movies
- Able to add/delete actors

# Executive Producer
- Can perform all operations that the Casting Director has
- Able to add/delete movies

## Getting Started
This app is hosted on Heroku and available in the following link:
http://casting-agency-appl.herokuapp.com/

The app can be also set up locally as well.

### Installing Dependencies

1. **Python 3.9** - Follow the documentation to install the lasted version of Python: [python docs] (https://www.python.org/downloads/)

2. **Miniconda** - Is highly recommended to use a virtual environment when using Python in your local machine to isolate dependencies per project. Follow the documentation to get this up and running: [conda docs] (https://docs.conda.io/en/latest/miniconda.html)

Once your environment is created, run the following line to activate it:
```
 conda activate environmentName
```

3. **Environment dependencies** - After your environment is created and activated, install the project's dependencies by navigating to the root directory and running:
```
pip install -r requirements.txt
```

4. **Key Dependencies**
- [Flask] (https://flask.palletsprojects.com/) is used to handle requests and responses. It's a lightweight backend microservices framwork.
- [jose] (https://python-jose.readthedocs.io/en/latest/) Used for verifying, encoding, and decoding Json Web Tokens (JWTs). Stands for JacaScript Object Signing and Endcryption.
- [SQLALchemy] (https://www.sqlalchemy.org/) Python ORM that will me used to manage PostgreSQL.
- [Flask-CORS] (https://flask-cors.readthedocs.io/en/latest/#) extension that will be used to manage CORS (cross origin requests).

### Database Setup
Start your [Postgres] (https://www.postgresql.org/download/) server:
```
pg_ctl -D /usr/local/var/postgres start
```

Now that Postgres is running in your local machine, create a database for local testing purposes, using the terminal
```
createdb casting-agency
```

Initialize your database restoring a backup provided in the casting-agency.psql file. Run in the terminal:
```
psql casting-agency < casting-agency.psql
```

### Running the Server

Make sure you have activated the virtual environment and proceed to export the environment variables you'll need, from the terminal:
```
source setup.sh
```

Run the server:

```
flask run --reload
```

please note, including the --reload flag will help restarting the server whenever changes are detected.

## Endpoints

**GET '/actors'**
- Fetches a list of dictionaries where each dictionary contains all the information corresponding to an actor
- Request Arguments: None
- Returns: a list of dictionaries, where each dictionary contains id, name, gender and birthday for a given author

****
{
    "actors": [
        {
            "birthdate": "Mon, 01 Jan 1990 00:00:00 GMT",
            "gender": "M",
            "id": 1,
            "name": "Adan Green"
        },
        {
            "birthdate": "Mon, 01 Jan 1990 00:00:00 GMT",
            "gender": "M",
            "id": 2,
            "name": "Mel Gibson"
        }
    ],
    "success": true
}
****


**GET '/movies'**
- Fetches a list of dictionaries where each dictionary contains all the information corresponding to a movie
- Request Arguments: None
- Returns: a list of dictionaries, where each dictionary contains id, title, and release date for a given movie

```
{
    "movies": [
        {
            "id": 1,
            "release_date": "Mon, 01 Jan 1990 00:00:00 GMT",
            "title": "The Passion of Christ"
        },
        {
            "id": 2,
            "release_date": "Mon, 01 Jan 1990 00:00:00 GMT",
            "title": "Alex was Found"
        }
    ],
    "success": true
}
```

**POST '/actors'**
- Sends a post request for the creation of a new actor
- Request Body: {"name": string, "birthdate":date, "gender": string (one character lenght, "M" or "F")}
- Returns: the id of the new created actor and the success (boolean) value

```
{
    "created": 3,
    "success": true
}
```

**POST '/movies'**
- Sends a post request for the creation of a new movie
- Request Body: {"title":string, "release_date": date}
- Returns: the id of the new created movie and the success (boolean) value

```
{
    "created": 3,
    "success": true
}
```

**DELETE '/actors/<int:actor_id>'**
- Sends a delete request to delete a given actor
- Request Arguments: actor_id (integer)
- Returns: the id of the deleted actor and the success (boolean) value

```
{
    "deleted": 4,
    "success": true
}
```

**DELETE '/movies/<int:movie_id>'**
- Sends a delete request to delete a given movie
- Request Arguments: movie_id (integer)
- Returns: the id of the deleted movie and the success (boolean) value

```
{
    "deleted": 4,
    "success": true
}
```

**PATCH '/actors/<int:actor_id>'**
- Sends a patch request to patch a given actor
- Request Arguments: actor_id (integer)
- Request Body: you may include the specific attributes you want to patch, format: {"name":string, "birthdate":date, "gender": string (one character lenght, "M" or "F")}
- Returns: an array that contains the specific actor that was patched

```
{
    "actors": [
        {
            "birthdate": "Mon, 01 Jan 1990 00:00:00 GMT",
            "gender": "M",
            "id": 2,
            "name": "Ana Bell"
        }
    ],
    "success": true
}
```

**PATCH '/movies/<int:movie_id>'**
- Sends a patch request to patch a given movie
- Request Arguments: movie_id (integer)
- Request Body: you may include the specific attributes you want to patch, format: {"title":string, "release_date":date}
- Returns: an array that contains the specific movie that was patched

```
{
    "movies": [
        {
            "id": 1,
            "release_date": "Wed, 01 Jan 2020 00:00:00 GMT",
            "title": "looking stars"
        }
    ],
    "success": true
}
```


## Testing
To run the available tests, run
```
dropdb casting-agency
createdb casting-agency
source setup.sh
psql casting-agency < casting-agency.psql
python3 test_app.py
```





