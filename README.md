# Simple Fullstack Blog web app

with CRUD interactions

## Technologies used

- NextJS
- NodeJS
- Express
- PostgreSQL
- RESTapi

## About

Use will have a option to log into the system and as logged user he can comment on to blog post in Markdown.
On some user will have role to create new blog posts and it will be writen in Markdown.

Unloged users will have only access to read articles.

## DB

```sql
-- Users table to store user information
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(100) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    role_id INT REFERENCES roles(id),  -- Foreign key referencing the roles table
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Roles table to manage different user permissions
CREATE TABLE roles (
    id SERIAL PRIMARY KEY,
    role_name VARCHAR(50) NOT NULL UNIQUE  -- E.g., 'user', 'admin', 'editor'
);

-- Blog posts table for storing articles
CREATE TABLE blog_posts (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,  -- Markdown content
    author_id INT REFERENCES users(id),  -- Foreign key referencing the users table
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Comments table for user comments on blog posts
CREATE TABLE comments (
    id SERIAL PRIMARY KEY,
    content TEXT NOT NULL,  -- Markdown content for the comment
    post_id INT REFERENCES blog_posts(id) ON DELETE CASCADE,  -- Foreign key referencing blog_posts
    user_id INT REFERENCES users(id),  -- Foreign key referencing the users table
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Example inserts for roles
INSERT INTO roles (role_name) VALUES ('user'), ('editor'), ('admin');

```
