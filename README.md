# Memories - A Social Media App

A full-stack social media application built with React, Redux, Node.js, Express, and MongoDB.

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/c87f638d-f5ed-4098-8f94-93c252bb453c" />


## Features

- **Create Posts** — Share memories with title, message, tags, and image
- **View Posts** — Browse all posts in a feed
- **Edit Posts** — Update post content
- **Delete Posts** — Remove posts you've created
- **Like Posts** — Like posts from other users
- **Image Upload** — Attach images to posts
- **Responsive UI** — Material-UI based design

## Tech Stack

### Frontend

- **React** — UI library
- **Redux** — State management
- **Redux Thunk** — Async actions
- **Axios** — HTTP client
- **Material-UI** — Component library

### Backend

- **Node.js** — Runtime
- **Express** — Web framework
- **MongoDB** — Database
- **Mongoose** — ODM (Object Data Modeling)
- **CORS** — Cross-Origin Resource Sharing
- **Body Parser** — Request parsing

## Project Structure

```
Social_media/
├── client/              # React frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── Form/    # Post creation form
│   │   │   └── Posts/   # Posts display and list
│   │   ├── actions/     # Redux actions
│   │   ├── reducers/    # Redux reducers
│   │   ├── api/         # Axios API calls
│   │   ├── App.js
│   │   └── index.js
│   └── package.json
├── server/              # Node/Express backend
│   ├── controllers/     # Route handlers
│   ├── models/          # Mongoose schemas
│   ├── routes/          # API routes
│   ├── index.js         # Entry point
│   ├── package.json
│   └── .env             # Environment variables
├── .gitignore
└── README.md
```

## Installation

### Prerequisites

- **Node.js** (v14+)
- **npm** (v6+)
- **MongoDB** (local or Atlas)

### Setup

1. **Clone or extract the project:**

   ```bash
   cd Social_media
   ```

2. **Install backend dependencies:**

   ```bash
   cd server
   npm install
   ```

3. **Install frontend dependencies:**

   ```bash
   cd ../client
   npm install
   ```

4. **Configure environment variables:**

   Create a `.env` file in the `server` folder:

   ```
   CONNECTION_URL=mongodb+srv://username:password@cluster.mongodb.net/?appName=Cluster0
   PORT=5000
   ```


## Running the Application

### Start Backend Server

```bash
cd server
npm start
```

Expected output:

```
Server running on port: 5000
```

### Start Frontend Development Server

In a new terminal:

```bash
cd client
npm start
```

The app will open at `http://localhost:3000`

## How It Works

### Frontend Flow (React + Redux)

1. **Initial Load** — User opens the app

   - Redux dispatches `getPosts()` action via Redux Thunk
   - Axios makes GET request to `/posts` endpoint
   - Posts data is fetched from backend and stored in Redux store

2. **Creating a Post** — User fills the form and submits

   - Form component captures: creator, title, message, tags, image
   - `createPost()` action is dispatched
   - Axios sends POST request with post data to backend
   - New post is added to Redux store
   - Form is reset

3. **Editing a Post** — User clicks edit on a post

   - Post ID and data are populated in the form
   - User modifies the content
   - `updatePost()` action is dispatched
   - Axios sends PATCH request to `/posts/:id`
   - Redux store is updated with new data

4. **Deleting a Post** — User clicks delete

   - `deletePost()` action is dispatched with post ID
   - Axios sends DELETE request to `/posts/:id`
   - Post is removed from Redux store

5. **Liking a Post** — User clicks like button
   - `likePost()` action is dispatched
   - Axios sends PATCH request to `/posts/:id/likePost`
   - Like count is updated in the store

### Backend Flow (Node.js + Express + MongoDB)

1. **Server Startup**

   - Express app initializes
   - dotenv loads environment variables
   - Mongoose connects to MongoDB
   - Routes are registered

2. **GET /posts** — Fetch all posts

   - Controller queries MongoDB for all posts
   - Returns posts array as JSON response

3. **POST /posts** — Create new post

   - Request body contains post data
   - New PostMessage document is created
   - Data is saved to MongoDB
   - Returns created post with ID

4. **PATCH /posts/:id** — Update post

   - Validates MongoDB ObjectId
   - Finds post by ID and updates with new data
   - Returns updated post

5. **DELETE /posts/:id** — Delete post

   - Validates MongoDB ObjectId
   - Finds and removes post from MongoDB
   - Returns success message

6. **PATCH /posts/:id/likePost** — Like post
   - Finds post by ID
   - Increments like count
   - Returns updated post

### Data Flow Diagram

```
User Action (UI)
      ↓
React Component
      ↓
Redux Action (Redux Thunk)
      ↓
Axios HTTP Request
      ↓
Express Route Handler
      ↓
MongoDB Controller
      ↓
MongoDB Database
      ↓
Response → Redux Store → Update UI
```

### State Management (Redux)

- **Actions** (`src/actions/Posts.js`) — Define async operations
- **Reducers** (`src/reducers/Posts.js`) — Update store based on actions
- **Store** (`src/index.js`) — Central state container with middleware

## API Endpoints

### Posts

- **GET** `/posts` — Fetch all posts
- **POST** `/posts` — Create a new post
- **PATCH** `/posts/:id` — Update a post
- **DELETE** `/posts/:id` — Delete a post
- **PATCH** `/posts/:id/likePost` — Like a post

## Environment Variables

### Server (.env)

```
CONNECTION_URL=your-mongodb-connection-string
PORT=5000
```


