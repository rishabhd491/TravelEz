# TravelEz
# Place Review and Favourites Project

This project allows users to search for places, add them to their favourites, and leave reviews. It is built using PHP, MySQL, HTML, CSS, and JavaScript.

## Features

- Display a list of places
- Add places to favourites
- Leave reviews for places
- Display top 10 reviews for each place

## Requirements

- PHP 7.4 or higher
- MySQL or MariaDB
- A web server (e.g., Apache or Nginx)

## Installation

1. Clone the repository to your local machine:
   ```sh
 git clone https://github.com/yourusername/your-repo-name.git
  cd your-repo-name

  2 Set up the database:

Create a database named my_project.
Run the following SQL commands to create the necessary tables:

CREATE DATABASE my_project;

USE my_project;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL
);

CREATE TABLE places (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT NOT NULL
);

CREATE TABLE favourites (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    place_id INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (place_id) REFERENCES places(id)
);

CREATE TABLE reviews (
    id INT AUTO_INCREMENT PRIMARY KEY,
    place_id INT NOT NULL,
    user_id INT NOT NULL,
    review TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (place_id) REFERENCES places(id),
    FOREIGN KEY (user_id) REFERENCES users(id)
);

Configure the database connection:

Create a connection.php file in the project root with the following content:
<?php
$host = '127.0.0.1';
$db = 'my_project';
$user = 'root';
$pass = '';
     $charset = 'utf8mb4';

$dsn = "mysql:host=$host;dbname=$db;charset=$charset";
$options = [
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    PDO::ATTR_EMULATE_PREPARES   => false,
];

try {
    $pdo = new PDO($dsn, $user, $pass, $options);
} catch (\PDOException $e) {
    throw new \PDOException($e->getMessage(), (int)$e->getCode());
}
?>

Start the PHP built-in server:

php -S localhost:8000

Open your browser and navigate to http://localhost:8000.

File Structure
index.php: Entry point of the project.
search.php: Displays the list of places with "like" and "review" buttons.
add_to_favourites.php: Handles AJAX requests to add places to favourites.
add_review.php: Handles AJAX requests to add reviews.
connection.php: Database connection configuration.
css/main.css: Styles for the project.
js/like.js: JavaScript for handling "like" button clicks.
js/review.js: JavaScript for handling "review" button clicks.
Usage
Navigate to the project URL in your browser.
The main page will display a list of places.
Click the "Like" button to add a place to your favourites.
Click the "Review" button to leave a review for a place.
The top 10 reviews for each place will be displayed below the "Review" button.
