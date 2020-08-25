# The Arena

 - [Description](#description)
- [Frontend](#frontend)
- [Backend](#backend)
- [Database](#database)
- [Web Ops](#web-ops)

# Description

This repository hosts the documentation for the full stack environment of The Arena, Inc.

# Frontend

```
frontend
├── public (publicly accessible resources)
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
├── src (application source code)
|   ├── Components
|   |   ├── Source files for application
|   ├── App.css
|   ├── App.jsx
├── package.json (project metadata)
├── node_modules (project dependencies)
```

### `npm run start`

Run the application in development mode. Open the application in [http://localhost:3000/](http://localhost:3000/) to view it. Lazy-loading is implemented in dev, meaning that the react server does not need to be restarted when edits are made.

### `npm run build`

Production grade build is created at `./build`. To run the production build, see [backend](#backend).

#### Note: upon cloning the repository, run `npm i` to install dependencies

# Backend

```
backend
├── api.py (web application)
├── error.log (error log)
├── app.yaml (used for deployment)
├── requirements.txt (used for deployment)
├── build (production grade build created in frontend)
│   ├── ...
```

## Dev Environment

### `flask run`

Runs the back-end environment in development. Default port is 5000, which interfaces with the frontend. Lazy-loading is implemented in dev, meaning that the backend does not need to be restarted when edits are made.


<sup>To change the proxy server on dev, navigate to `./frontend/package.json`, scroll to the bottom until you see `"proxy": "http://localhost:5000"`, and change to whatever port you are running the backend on.</sup>

## Production Environment

### Building and deploying the application

1. [Build the react app](#npm-run-start)
2. Copy the build directory from `frontend` to the `backend` directory (should be on the same directory level as `api.py`). Make sure you do not change the name of the directory from `build`, otherwise the web app will not be able to serve the static build.
3. Deploy the application to app engine:

```bash
bash-3.2$ pwd
/Users/thearena/backend
bash-3.2$ ls
README.md  __pycache__  api.py  app.yaml  build error.log  requirements.txt
bash-3.2$ gcloud app deploy
Services to deploy:
descriptor:  [/Users/thearena/backend/app.yaml]
source:  [/Users/thearena/backend]
target project:  [training-program-database]
target service:  [default]
target version:  [20200824t231953]
target url:  [https://training-program-database.uc.r.appspot.com]

Do you want to continue (Y/n)?
```

**Hit Y and then let the deployment proceed. This make take anywhere from 10 minutes to an hour.**


# Routes ([API](#Backend))

This section details the API endpoints for the application

## Search For Program

#### `POST /api/search_program`

Search the database based on a query string. Return search results

**Params:**

| param | type | description | long description |
| - | - | - | - |
| query | string  [required] | Search string | <p align="center">The query is the search string that the DB is being queried for. Example: `"Bachelor's healthcare"`.</p>
 
`curl -X POST -d '{"query": "bachelor healthcare"}' -H 'Content-Type: application/json' /api/search_program`

 **Note:** This request uses `'Content-Type: application/json'`.

## Query Programs

#### `POST /api/programs`

Identify programs based on designated field values.

**Params:**

| param | type | description | long description |
| - | - | - | - |
| field | array | Designated field | <p align="center">The number of fields in the POST may vary. Each field corresponds to a database parameter.
.</p>

```json
curl -X POST -d '
'{
	"outcome": ["skill", "certificate"], 
	"budget": {
		"start": 0, 
		"end": 5000
	}
}'
 -H 'Content-Type: application/json' /api/programs
```

**Note:** The field `budget` accepts an object of the format shown above. This request uses `'Content-Type: application/json'`.

## Get Program (by id)

#### `POST /api/program`

Return program from database + related programs.

**Params:**

| param | type | description | long description |
| - | - | - | - |
| id | integer  [required] | Program ID | <p align="center">Unique ID of the program</p>
 
`curl -X POST -d '{"id": 258}' -H 'Content-Type: application/json' /api/search_program`

 **Note:** This request uses `'Content-Type: application/json'`.
