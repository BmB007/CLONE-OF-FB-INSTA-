# ConnectMe - Social Media Platform

## Description

ConnectMe is a social media platform similar to Facebook, built using Node.js, Express, and MongoDB. It provides user authentication, profile management, friend requests, and post management.

## Features

* **User Authentication:** User registration and login with JWT authentication.
* **Profile Management:** Users can view and update their profiles, including profile pictures and privacy settings.
* **Friend Requests:** Users can send, accept, and remove friend requests.
* **Post Management:** Users can create, view, like, and delete posts.
* **Image Uploads:** Profile pictures and post images can be uploaded.

## Technologies Used

* Node.js
* Express
* MongoDB
* Mongoose
* bcryptjs
* jsonwebtoken
* express-validator
* multer
* cors
* dotenv

* ## Upcoming Features

* **Accept requests:** 2 line buffers in single page for this feature
* **Mail Authentication:** Authenticity of the mail while registering into Photogram.

## Installation

1.  **Clone the repository:**

    ```bash
    git clone <repository_url>
    ```

2.  **Install dependencies:**

    ```bash
    npm install
    ```

3.  **Set up environment variables:**

    * Create a `.env` file in the root directory.
    * Add the following environment variables:    
        ```
        PORT=5000
        MONGO_URI=mongodb://localhost:27017/connectme
        JWT_SECRET=your_jwt_secret_key_here
        JWT_EXPIRE=30d
        ```
        Note: The IP address (using ADD IP adrdress) and Secret key (any key) to be updated after installation.

    * Replace `your_jwt_secret_key_here` with your actual secret key.  **IMPORTANT:  Keep this secret!**

4.  **Start the server:**

    ```bash
    npm run dev # For development with nodemon
    npm start   # For production
    ```

    The server will be running at `http://localhost:5000`.

## Database Setup

* Ensure you have MongoDB installed and running.
* The `MONGO_URI` in the `.env` file should point to your MongoDB database.  The default is `mongodb://localhost:27017/connectme`.  You can change the database name (`connectme`) if you like.

## API Endpoints

### Authentication

* `POST /api/auth/register`: Register a new user.
    * **Body:** `{ username, email, password }`
* `POST /api/auth/login`: Log in and get a JWT token.
    * **Body:** `{ email, password }`
* `GET /api/auth/me`: Get the current user's information (requires authentication).
    * **Headers:** `Authorization: Bearer <token>`

### Users

* `GET /api/users`: Get all users (requires authentication).
    * **Headers:** `Authorization: Bearer <token>`
* `GET /api/users/:id`: Get a user by ID.
    * **Headers:** `Authorization: Bearer <token>`  (May be required depending on profile privacy)
* `PUT /api/users/profile`: Update the user's profile.
    * **Headers:** `Authorization: Bearer <token>`
    * **Body:** `{ bio, visibility }`  (`visibility` can be "public", "friends", or "private")
* `PUT /api/users/profile-picture`: Update the user's profile picture.
    * **Headers:** `Authorization: Bearer <token>`
    * **Form-data:** `profilePicture` (file)
* `POST /api/users/friend-request/:id`: Send a friend request to a user.
    * **Headers:** `Authorization: Bearer <token>`
* `PUT /api/users/accept-request/:id`: Accept a friend request.
    * **Headers:** `Authorization: Bearer <token>`
* `DELETE /api/users/friend/:id`: Remove a friend.
    * **Headers:** `Authorization: Bearer <token>`

### Posts

* `POST /api/posts`: Create a new post.
    * **Headers:** `Authorization: Bearer <token>`
    * **Body:** `{ text, image }` (image is optional, send as form-data if including)
* `GET /api/posts`: Get all posts.
    * **Headers:** `Authorization: Bearer <token>`
* `GET /api/posts/:id`: Get a post by ID.
     * **Headers:** `Authorization: Bearer <token>`
* `PUT /api/posts/like/:id`: Like/unlike a post.
    * **Headers:** `Authorization: Bearer <token>`
* `DELETE /api/posts/:id`: Delete a post
     * **Headers:** `Authorization: Bearer <token>`

## Authentication

* Most user and post-related routes are protected and require a valid JWT token in the `Authorization` header.
* The token should be sent as a `Bearer` token:

    ```
    Authorization: Bearer <your_token_here>
    ```

## Error Handling

* The API returns JSON error responses with appropriate HTTP status codes.
* Validation errors are returned as an array of errors.
* Server errors return a 500 status code.

## File Structure

connectme/├── config/│   └── db.js       # Database connection├── controllers/│   ├── authController.js    # User authentication│   ├── postController.js    # Post management│   └── userController.js    # User profile management├── middleware/│   └── auth.js       # Authentication middleware├── models/│   ├── Post.js       # Post model│   └── User.js       # User model├── routes/│   ├── auth.js       # Authentication routes│   ├── posts.js      # Post routes│   └── users.js      # User routes├── uploads/          # Store uploaded files├── .env              # Environment variables├── app.js            # Main application file├── package.json      # Project dependencies└── README.md         # Documentation
##  Important Considerations

* **Security:** The provided `.env` file should **not** be committed to version control.  Use a secure method to manage your environment variables (e.g., environment variables on your server, a dedicated secrets management tool).  The `JWT_SECRET` should be a strong, unique secret.
* **File Uploads:** The `uploads/` directory is where uploaded files (profile pictures, post images) are stored.  Ensure this directory has appropriate permissions.
* **Error Handling:** The application includes basic error handling, but you may want to add more robust error logging and handling for a production environment.
* **Validation:** The `express-validator` package is used for input validation.  Ensure that all API endpoints have proper validation to prevent unexpected data.
* **Database:** The application uses MongoDB.  Make sure your MongoDB instance is running and the connection URI is correctly configured in the `.env` file.
* **Scalability:** For a production application, consider using a process manager like PM2, setting up a reverse proxy (e.g., Nginx), and potentially using a more scalable database solution.
* **Comments**: The code is well commented, explaining the purpose of each file, function, and route.
* **Fixed path issues and module import errors**: The initial comment in the provided code indicates that path and module import errors have been resolved.
* **Dependencies**:  All dependencies are listed in `package.json`.
* **Environment variables**:  The `.env` file is provided with the necessary variables.
* **Database connection**:  The `config/db.js` file handles the database connection.
* **Controllers**:  The `controllers/` directory contains the logic for each API endpoint.
* **Routes**:  The `routes/` directory defines the API routes.
* **Models**:  The `models/` directory defines the database schemas.
* **Middleware**:  The `middleware/auth.js` file contains the authentication middleware.
* **Error handling middleware**:  Error handling middleware is included in `app.js`.
