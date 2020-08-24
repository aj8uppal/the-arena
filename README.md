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
|   ├── App.css
|   ├── App.js
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

### `flask run`

Runs the back-end environment in development. Default port is 5000, which interfaces with the frontend. Lazy-loading is implemented in dev, meaning that the backend does not need to be restarted when edits are made.


<sup>To change the proxy server on dev, navigate to `./frontend/package.json`, scroll to the bottom until you see `"proxy": "http://localhost:5000"`, and change to whatever port you are running the backend on.</sup>

# Routes (API)

This section details the API endpoints for the application

## Search Program

#### `POST /api/search_program`

Search the database based on a query string. Return search results

**Params:**

| param | type | description | long description |
| - | - | - | - |
| query | string  [required] | Search string | <p align="center">The query is the search string that the DB is being queried for. Example: `"Bachelor's healthcare"`.</p>
 
`curl -X POST -d '{"query": "bachelor healthcare"}' -H 'Content-Type: application/json' /api/search_program`

 **Note:** This request uses `'Content-Type: application/json'`.

## Find Provider

#### `POST /api/providers`

Identify providers based on designated field values.

**Params:**

| param | type | description | long description |
| - | - | - | - |
| field | varies | Designated field | <p align="center">The number of fields in the POST may vary. Each field corresponds to a database parameter. For example, </p>
