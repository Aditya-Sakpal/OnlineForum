![fullstack-graphql](https://raw.githubusercontent.com/atulmy/atulmy.github.io/master/images/mix/dev-logos.png)

# Fullstack GraphQL

Simple Demo Application

**API** built with Node + Express + GraphQL + Sequelize (supports MySQL, Postgres, Sqlite and MSSQL). 

**WebApp** built with React + Redux. 

Written in ES6 using Babel + Webpack.

## 📝 Features
- [x] List thoughts
- [x] Add thought
- [x] Delete thought
- [x] View single thought

## ▶️ Running
- Clone repo `git clone git@github.com:atulmy/fullstack-graphql.git fullstack-graphql`
- Install NPM modules API `cd api` and `npm install`
- Install NPM modules Webapp `cd web` and `npm install`
- Modify `/api/src/config/database.json` for database credentials
- Modify `/api/src/config/config.json` for API port (optional)
- Modify `/web/.env` for web port (optional)
- Run API `cd api` and `npm start`, browse GraphiQL at http://localhost:8000/
- Run Webapp `cd web` and `npm start`, browse web at http://localhost:3000/

### Sample API logs
```
[nodemon] starting `babel-node src/index.js --presets es2015,stage-2`
SETUP - Connecting database...
SETUP - Loading modules...
SETUP - GraphQL...
SETUP - Syncing database tables...
INFO - Database connected.
INFO - Database sync complete.
SETUP - Starting server...
INFO - Server started on port 3000.
```

## 📸 Screenshots
![screenshot](http://atulmy.com/atulmy.com/attachments/images/fullstack-graphql.gif?v=0.1)

## 🏗 Core Structure
    fullstack-graphql
      ├── api (api.example.com)
      │   ├── src
      │   │   ├── config
      │   │   ├── models
      │   │   ├── schema
      │   │   ├── setup
      │   │   └── index.js
      │   │
      │   └── package.json
      │
      ├── web (example.com)
      │   ├── public
      │   ├── src
      │   │   ├── components
      │   │   ├── setup
      │   │   └── index.js
      │   │
      │   ├── .env
      │   └── package.json
      │
      ├── .gitignore
      └── README.md

## 📘 Guides
### API
- Adding new Module (Eg: Users):
  - Copy `/api/src/models/thought.js` to `/api/src/models/user.js` and modify the file for table name and respective fields
  - Add an entry to the `models` object in `/api/src/models/index.js`
  - Copy `/api/src/schema/thoughts` to `/api/src/schema/users` and modify `type.js`, `resolvers.js` and `fields/query.js` and `fields/mutations.js`
  - Import `/api/src/schema/users/fields/query.js` in `/api/src/schema/query.js`
  - Import `/api/src/schema/users/fields/mutations.js` in `/api/src/schema/mutations.js`

### Webapp
- Adding new Module (Eg: Users):
  - Create folder `users` under `/web/src/components/`
  - Create your Container and Resusable components under `/web/src/components/users`
  - Create `api` folder under `/web/src/components/users`
  - Add `actions.js` where all your Redux Action Types and Actions will reside (refer `/web/src/components/thoughts/api/actions.js`)
  - Add `state.js` where all your respective Reducers will recide (refer `/web/src/components/thoughts/api/state.js`)
  - Import the module state in `/web/src/setup/store.js` to make it avaliable to the app
  - Encapsulate all your User related code in `/web/src/components/users`
- Adding new Route (Eg: `/users`):
  - Add a new entry to `routes` object in `/web/src/setup/routes.js` (eg `user: { list: '/list' }`)
  - Edit `/web/src/components/App.js` and add the route entry

<table width="100%" style="width: 100%">
    <tbody>
        <tr valign="top">
            <td width="50%" style="width: 50%">
                <p>Query - Get List</p>
                <pre>
query {
  thoughts {
    id,
    name,
    thought
  }
}
                </pre>
            </td>
            <td width="50%" style="width: 50%">
                <p>Response</p>
                <pre>
{
  "data": {
    "thoughts": [
      {
        "id": 1,
        "name": "Arya Stark",
        "thought": "A girl has no name"
      },
      {
        "id": 2,
        "name": "Jon Snow",
        "thought": "I know nothing"
      }
    ]
  }
}
                </pre>
            </td>
        </tr>
        <tr></tr>
        <tr valign="top">
            <td>
                <p>Query - Get by Param</p>
                <pre>
query {
  thought(id: 1) {
    id,
    name,
    thought
  }
}
                </pre>
            </td>
            <td>
                <p>Response</p>
                <pre>
{
  "data": {
    "thought": {
      "id": 1,
      "name": "Arya",
      "thought": "A girl has no name"
    }
  }
}
                </pre>
            </td>
        </tr>
        <tr></tr>
        <tr valign="top">
            <td>
                <p>Mutation - Create</p>
                <pre>
mutation {
  thoughtCreate(
    name: "Tyrion Lannister", 
    thought:"I drink and I know things"
  ) {
    id
  }
}
                </pre>
            </td>
            <td>
                <p>Response</p>
                <pre>
{
  "data": {
    "thoughtCreate": {
      "id": 3
    }
  }
}
                </pre>
            </td>
        </tr>
        <tr></tr>
        <tr valign="top">
            <td>
                <p>Mutation - Remove</p>
                <pre>
mutation {
  thoughtRemove(id: 3) {
    id
  }
}
                </pre>
            </td>
            <td>
                <p>Response</p>
                <pre>
{
  "data": {
    "thoughtRemove": {
      "id": null
    }
  }
}
                </pre>
            </td>
        </tr>
    </tbody>
</table>
