# Todo-List

## Introduction
This ToDoList web app allows users manage their tasks efficiently. System includes authentication functionalities through login and a dashboard page where can view and manage tasks.

## Technologies Used
* HTML: Web pages structure.
* CSS: Personalized styles for a modern and friendly UI.
* JavaScript: App logic, backend interaction through Axios.
* Axios: Realization of HTTP requests to the backend.
* API REST: Backend for users and tasks management.

## Project Structure
* `index.html`: Home page with a login form.
* `./css/login.css`: Login form style.
* `./scripts/login.js`: Login logic with the API conection.
* `dashboard.html`: User panel where handles tasks.
* `./css/styledash.css`: Dashboard page style.
* `./scripts/scriptdash.js`: Dashboard logic and tasks update.

## General Use
1. Access to app.
    * Can enter by URL: https://terasoluciones.com.mx/Angel

2. Access to Login Page
    * Introduce user name and PIN. 
    * Press Login button.

3. Dashboard Redirection
    * If credentials are valid, user will be redirected to dashboard.
    * Into the dashboard can view and manage tasks.

## Requeriments
* A pc or smartphone with internet access.
* A navigator web like Opera, Google, Edge, Firefox, etc.

## Files Documentation
### Login Page
### index.html
Main file that contains the login form structure.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>

    <!-- CSS archive link for form design -->
    <link rel="stylesheet" href="./css/login.css" />

    <!-- Axios import for HTTP requests handling -->
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  </head>
  <body>
    <div class="container">
      <!-- Container for form image -->
      <div class="image-container"></div>
      
      <!-- Form container -->
      <div class="form-container">
        <header>
          <h1>Login</h1>
          <h5>Welcome back! Please login to your account.</h5>
        </header>

        <!-- Input field for username -->
        <div class="form-group">
          <label for="username">Username</label>
          <input type="text" id="username" placeholder="Enter username" />
        </div>

        <!-- Input field for PIN -->
        <div class="form-group">
          <label for="pin">PIN</label>
          <input type="password" id="pin" placeholder="Enter PIN" />
        </div>

        <!-- Button that runs login function -->
        <button onclick="login()">Login</button>
      </div>
    </div>
  </body>

  <!-- JavaScript archive for form functions -->
  <script src="./scripts/login.js"></script>
</html>
```

#### Form Structure:
* `Header`: Includes the title and description of the login.
* `Inputs`: Fields to enter `username` and `PIN`.
* Login Button: Actives authentication function.

#### Mains Sections:
* `container`: General container of form and bottom picture (`form-container` and `image-container`).
* `form-container`: Contians fields for `username` and `PIN`.
* `image-container`: Box which contains an image with colors according to the dashboard.
* `button`: Button has an `onclick()` event that runs `login()` function defined in the `login.js` file

### login.js
This code manage login functionality for the app.
   It uses URL API `https://terasoluciones.com.mx/todolist/API/index.php` for authenticate the users.

```javascript
const apiBaseUrl = 'https://terasoluciones.com.mx/todolist/API/index.php';

async function login() {
    // Obtain form values
    const username = document.getElementById('username').value;
    const pin = document.getElementById('pin').value;
    
    try {
        // Make the POST request to the API for login
        const response = await axios.post(`${apiBaseUrl}/login`, {username, pin});
        console.log(JSON.stringify(response.data));
        
        // Verify if login is successful
        if (response.data.user_id) {
            // Saves user ID and PIN in the local storage
            localStorage.setItem('user_id', response.data.user_id);
            localStorage.setItem('pin', pin);
            
            // Redirect user to dashboard page
            window.location.href = 'dashboard.html';
        } else {
            alert('Login failed: User ID not found');
        }
    } catch (error) {
        // Handle any error from request
        alert('Login failed: ' + (error.response?.data?.error || error.message));
    }
}
```

#### Explication:
1. Get the form data: The values of username and PIN are obtained through the form fields.
2. Request authentication: A POST request is sent to the API URL with the user and PIN data.
3. Verify the result: If the API responds with a user_id, the user is considered authenticated, and it is stored in the browser's local storage.
4. Redirection: If the login is successful, the user is redirected to the dashboard.html page.
5. Error handling: In case of an error, an alert is shown with the corresponding message.

#### Dependency:
* Axios: This code uses `axios` library to make HTTP requests. The library must be included in the HTML for it to work correctly.
`<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>`

#### Use instructions:
1. Login form: The `login()` function is tiggered when clicking the login button, which must be associated with this script.
2. API configuration: Make sure the API base URL is correctly configured and accessible from the browser.

### login.css
This set of CSS rules defines the visual style for the login page. It ensures the page is aesthetically pleasing, functional, and responsive across different screens sizes.

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #1E293B;
  padding: 1rem;
}

h1 {
  padding-bottom: 1rem;
}

h5 {
  color: #babac6;
  font-weight: normal;
  margin-bottom: 2rem;
}

.container {
  display: flex;
  background-color: white;
  max-width: 800px;
  width: 100%;
  min-height: 400px;
  border-radius: 10px;
  box-shadow: 0 0 30px rgb(0, 0, 0);
  overflow: hidden;
  font-size: smaller;
}

.image-container {
  position: relative;
  flex: 1;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #334155;
}

.image-container::before {
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  background-image: url("https://images.pexels.com/photos/6985124/pexels-photo-6985124.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1");
  background-size: cover;
  background-position: left;
  background-repeat: no-repeat;
}

.form-container {
  flex: 1;
  padding: 3rem;
  min-width: 300px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background-color: #334155;
}

header {
  display: flex;
  flex-direction: column;
  margin-bottom: 3rem;
  color: white;
}

.form-group {
  margin-bottom: 1.5rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  color: #94A3B8;
}

input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 1rem;
}

input:focus {
  outline: none;
  border-color: #4caf50;
  box-shadow: 0 0 5px rgba(76, 175, 80, 0.2);
}

button {
  width: 100%;
  padding: 0.75rem;
  background-color: #10B981;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
  transition: filter 0.3s ease;
}

button:hover {
  filter: brightness(0.7);
}

@media (max-width: 768px) {
  .container {
    flex-direction: column;
    min-height: auto;
  }

  .image-container {
    height: 300px;
  }

  .form-container {
    padding: 2rem;
  }
}

@media (max-width: 480px) {
  .image-container {
    height: 200px;
  }

  .form-container {
    padding: 1.5rem;
  }
}
```

#### Explanation:
1. Reset Margin and Padding: The `*` selector ensures that all elements have zero margin and padding, avoiding any unexpected behavior in the layout.
2. Basic Styles:
    * The `body` takes up the full height of the screen with a minimum height of 100vh, using `flex` to center the content.
    * The background color is dark (`#1E293B`), while the text in headers (`h1`, `h5`) is light.
3. Main Layout:
    * `.container`: Uses `flex` to arrange the content into two columns: one for the image and one for the form.
    * `.image-container`: The background image covers the entire space and is cropped using `background-size: cover`
4. Form:
    * The form fields are styled with a clean design, soft borders, and light background.
    * The `input` fields have a focus effect, changing the border and adding a subtle shadow when clicked.
    * The button has a bright green color and changes when hovered over (`hover` effect).
5. Responsiveness:
    * The `@media` queries adjust the layout for different screen size:
        * On screens with a width of 768px or smaller, the layout switches to a column format.
        * On screens with a width of 480px or smaller, the image and form container sizes are adjusted further.

#### Use instructions:
1. HTML: Make sure to link this CSS file in your HTML for the login page.
`<link rel="stylesheet" href="./css/login.css" />`

## Dashboard Page
### dashboard.html
This HTML structure represents the dashboard page where users can add tasks and view pending tasks. The page is interactive and allows users to manage tasks via dynamic forms and tables.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Character encoding and viewport settings for responsiveness -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    
    <!-- External CSS files -->
    <link rel="stylesheet" href="./css/styledash.css">
    
    <!-- Font Awesome for icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <!-- Axios library for HTTP requests -->
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
</head>
<body>
    <!-- Header Section: Contains the page title -->
    <header>
        <h1>Dashboard</h1>
    </header>
    
    <!-- Main Content Section -->
    <main>
        <!-- Button to show/hide the form for adding a new task -->
        <button class="add-button" onclick="toggleForm()">
            <!-- Font Awesome icon for adding a new task -->
            <i class="fas fa-plus"></i>
        </button>

        <!-- Form Section: Contains the form for adding a new task -->
        <section class="form-section">
            <!-- Button to hide the form when it's open -->
            <button class="hide-section" onclick="toggleForm()">
                <!-- Font Awesome icon for toggling the form visibility -->
                <i class="fas icon-toggle"></i>
            </button>

            <h3>Add New Task</h3>
            
            <!-- Task description input field -->
            <div class="form-group">
                <label for="description">Description</label>
                <input type="text" id="description" placeholder="Task Description">
            </div>
            
            <!-- Start date input field -->
            <div class="form-group">
                <label for="start_date">Start Date</label>
                <input type="date" id="start_date">
            </div>
            
            <!-- End date input field -->
            <div class="form-group">
                <label for="end_date">End Date</label>
                <input type="date" id="end_date">
            </div>
            
            <!-- Photo input field to upload an image related to the task -->
            <div class="form-group">
                <label for="photo">Photo</label>
                <input type="file" id="photo" accept="image/*" capture="environment">
            </div>

            <!-- Button to submit the task data and call the addTask() function -->
            <button onclick="addTask()">Add Task</button>
        </section>

        <!-- Dashboard Section: Displays a table of pending tasks -->
        <section class="dashboard-section">
            <h3>Pending Tasks</h3>
            <table>
                <thead>
                    <tr>
```

#### Explanation:
1. Header Section:
    * The `<header>` contains the main title of the page `Dashboard`.
2. Add New Task Button:
    * A button with the class `add-button` that triggers the `toggleForm()` function to show the task addition form when clicked. It uses an icon from Font Awesome (`<i class="fas fa-plus"></i>`).
3. Task form :
* A `section` containing a form to add a new task, including fields for:
    * Description: A text input for the task description.
    * Start Date: A date input for selecting the task's start date.
    * End Date: A date input for selecting the task's end date.
    * Photo: A file input for uploading a photo related to the task. This input is specifically for capturing images from the environment (using the `capture="environment"` attribute).
* A button that calls `addTask()` to save the task.
4. Pending Tasks Section:
    * A `<section>` displaying the pending tasks in a table format.
    * The table contains headers for Description, Start Date, End Date, and Actions. The list of tasks will be dynamically inserted in the `<tbody>` with the id `task-list`.
5. Font Awesome Icons:
    * The page uses Font Awesome icons for the task form and toggle button.
6. External Libraries:
    * Font Awesome: For icons in the page (linked in the `<head>`)
    * Axios: For making HTTP requests (also linked in the `<head>`)
7. Dynamic Task List:
    * The task list is expected to be dynamically populated by JavaScript (`./scripts/scriptdash.js`), which will handle user interactions and load tasks from the API or local storage.

### styledash.css

```css
/* Reset all margin, padding, and box-sizing properties for consistency */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* General body styling */
body {
  font-family: Arial, sans-serif;
  background-color: #2D3748; /* Dark background */
  position: relative;
  min-height: 100vh;
}

/* Header styling */
header {
  background-color: #10B981; /* Green background */
  padding: 1rem;
  color: white;
}

/* Dashboard section header styling */
.dashboard-section h3 {
  margin-top: 1.2rem;
  margin-bottom: 1rem;
  color: #F3F4F6; /* Light gray text */
}

/* Main section containing form and tasks */
main {
  padding: 1rem;
  display: flex; /* Flexbox for layout */
  gap: 2rem;
  position: relative;
}

/* Form section styling */
.form-section {
  background: white; /* White background */
  padding: 1.5rem;
  border-radius: 10px 0px; /* Rounded corners */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Subtle shadow */
  width: 300px;
  transition: transform 0.3s ease; /* Smooth transition for visibility toggle */
}

/* Hide button section inside the form */
.hide-section {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    padding: 20px;
}

/* Dashboard section that holds the task table */
.dashboard-section {
  flex: 1; /* Takes up remaining space */
}

/* Form group styling */
.form-group {
  margin-bottom: 1rem;
}

/* Label styling for inputs */
label {
  display: block;
  margin-bottom: 0.5rem;
  color: #333; /* Dark text */
}

/* Common input and button styling */
input,
button {
  width: 100%;
  padding: 0.75rem;
  margin-top: 0.25rem;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #D1D5DB; /* Light gray background */
}

/* Button styling */
button {
  background-color: #10B981; /* Green background */
  color: white;
  cursor: pointer;
  font-size: large;
  border: none;
  transition: filter 0.3s ease; /* Transition for hover effect */
}

/* Button hover effect */
button:hover {
  filter: brightness(0.7); /* Darkens the button */
}

/* Table styling */
table {
  width: 100%;
  border-collapse: collapse; /* Makes table borders collapse */
  background: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Subtle shadow */
}

/* Table header styling */
th,
td {
  padding: 0.75rem;
  text-align: left;
}

th {
  background-color: #9B2C2C; /* Dark red header background */
  color: #ffffff;
}

tbody {
  background-color: #3E4C59; /* Dark gray body background */
  color: #E2E8F0; /* Light gray text */
}

/* Add button styling (floating button for adding a new task) */
.add-button {
  position: fixed;
  width: 60px;
  height: 60px;
  border-radius: 30%; /* Circular button */
  background: #F87171; /* Red background */
  color: white;
  display: none; /* Hidden by default */
  align-items: center;
  justify-content: center;
  cursor: pointer;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.); /* Light shadow */
}

.add-button i {
  font-size: 24px;
}

/* Icon toggle styling for showing/hiding form */
.icon-toggle::before {
  font-weight: 900;
  content: "\f078"; /* Font Awesome icon for "arrow down" */
}

/* Mobile Styles */
@media (max-width: 768px) {
  main {
    flex-direction: column; /* Stack items vertically on small screens */
  }

  /* Form section for mobile - fixed at the bottom */
  .form-section {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    transform: translateY(100%); /* Initially offscreen */
    z-index: 1000;
    margin: 0;
    border-radius: 20px 20px 0 0;
    background-color: #677486; /* Dark background */
  }

  .form-section.active {
    transform: translateY(0); /* Slide in when active */
  }

  /* Add button visible on mobile screens */
  .add-button {
    display: flex;
    bottom: 20px;
    right: 20px;
    z-index: 100;
  }
  
  /* Hide section button in mobile view */
  .hide-section {
    justify-content: flex-end;
    position: absolute;
    right: 30px;
    top: 9px;
    width: fit-content;
    color: black;
    font-size: larger;
    background-color: #677486; /* Background color for mobile form */
  }
}

/* Desktop Styles */
@media (min-width: 769px) {
  /* Form section for desktop - fixed on the left */
  .form-section {
    transform: translateX(-100%); /* Initially offscreen */
    position: fixed;
    height: calc(100vh - 70px);
    top: 70px;
    left: 0;
    overflow-y: visible;
    background-color: #677486; /* Dark background */
    z-index: 1;
  }

  .form-section.active {
    transform: translateX(0); /* Slide in when active */
  }

  /* Add button for desktop */
  .add-button {
    display: flex;
    margin-top: 78px;
    left: 30px;
    transform: translateY(-50%);
  }

  /* Adjust dashboard section layout for desktop */
  .dashboard-section {
    margin-left: 120px;
    margin-right: 20px;
  }

  /* Change icon for hiding the form on desktop */
  .icon-toggle::before {
    content: "\f053"; /* Font Awesome icon for "arrow left" */
  }

  /* Hide section button for desktop */
  .hide-section {
    display: none;
    justify-content: flex-end;
    position: absolute;
    padding-left: 11px;
    right: -43px;
    top: -4px;
    width: fit-content;
    color: black;
    font-size: larger;
    background-color: #677486;
    z-index: 9999;
    border-radius: 0px 8px 8px 0px;
  }

  /* Show hide section button when form is active */
  .form-section.active .hide-section {
    display: block;
  }
}
```

#### Explanation:
1. General Reset and Box Model:
    * The global `*` selector resets margin, padding, and sets the `box-sizing` to `border-box` for all elements to ensure a consistent layout across different browsers.
2. Body Styling:
    * The `body` is styled with a background color (`#2D3748`), set to `position: relative` for flexibility, and `min-height: 100vh` to cover the full viewport height. The default font is set to Arial, and sans-serif as a fallback.
3. Header Section:
    * The `header` contains the main title (`Dashboard`) and has a green background (`#10B981`) with white text. It uses padding to create spacing inside the header.
4. Dashboard Section Title: 
    * The `.dashboard-section h3` styles the headers inside the task table, setting the text color to light gray (`#F3F4F6`) and defining top and bottom margins to separate it from surrounding content.
5. Main Section Layout:
    * The `.form-section` defines the form area with a white background and rounded corners (`border-radius: 10px 0px`). It also includes a subtle shadow for depth and sets a transition for a smooth transformation effect when toggled.
6. Form Section Styling:
    * The `.form-section` defines the form area with a white background and rounded corners (`border-radius: 10px 0px`). It also includes a subtle shadow for depth and sets a transition for a smooth transformation effect when toggled.
7. Hide Section Button:
    * The `.hide-section` is used inside the form section to provide a button to close the form. It’s positioned at the top-right and uses flexbox for alignment.
8. Input and Button Styling:
    * Both the `input` and `button` elements are styled with full width, padding, and a border-radius for rounded corners. The background color is light gray (`#D1D5DB`), and the buttons have a specific green color (`#10B981`) with a hover effect that darkens the button on mouseover.
9. Table Styling for Pending Tasks:
    * The `table` is styled to have a clean, collapsed border layout. It has a white background, rounded corners, and a shadow for depth. Table headers are given a red background (`#9B2C2C`), with white text, while the table body has a dark gray background (`#3E4C59`) and light gray text (`#E2E8F0`).
10. Add Task Button Styling:
    * The `.add-button` is a floating button, styled to be circular (`border-radius: 30%`) with a red background (`#F87171`). It’s positioned at the bottom-right of the screen and has a box-shadow for better visibility. This button remains hidden until activated.
11. Responsive Design: 
    * Mobile Styles (`max-width: 768px`)
        * The main content is stacked vertically (`flex-direction: column`).
        * The form section is fixed at the bottom of the screen and can slide in from the bottom when active.
        * The `add-button` is positioned at the bottom-right corner for easy access on mobile.
    * Desktop Styles (`min-width: 769px`):
        * The form section is fixed on the left side and can slide in from the left when active.
        * The dashboard section is given left margin to make space for the form on the left.
12. Font Awesome Icons:
    * Font Awesome icons are used for the "Add Task" button and the toggle button for showing/hiding the form. The specific icons are `fa-plus` for the `add button` and `fa-arrow-left` for the hide button.
13. External Libraries:
    * The CSS does not directly link external libraries, but Font Awesome is used for icons, which are linked in the HTML `<head>`. Axios is also used for API calls, linked in the HTML but not relevant to the CSS itself.
14. Smooth Transition Effects:
    * The `transition` property is applied to form visibility changes, which slide the form in and out smoothly based on whether the 
    `.active` class is toggled. This is used in both mobile and desktop views.
15. Task List and Add Task Button Visibility:
    * The task list is dynamically populated by JavaScript, and the visibility of the "Add Task" button and form is controlled by JavaScript. On mobile, the form slides in from the bottom, and on desktop, it slides in from the left.

### scriptdash.js

```javascript
// Define the base URL for the API
const apiBaseUrl = 'https://terasoluciones.com.mx/todolist/API/index.php';
// Retrieve user ID and PIN from localStorage
const userId = localStorage.getItem('user_id');
const pin = localStorage.getItem('pin');

// Function to load tasks from the API and display them in the task list
async function loadTasks() {
    let respone; // A typo in the variable name, should be 'response'
    try {
        // Send a GET request to the API to retrieve tasks
        response = await axios.get(`${apiBaseUrl}/tasks`, {params:{user_id: userId, pin}});
        console.log(JSON.stringify(response)); // Log the response for debugging
        const tasks = response.data;
        const taskList = document.getElementById('task-list');
        taskList.innerHTML = ''; // Clear the current list of tasks

        // Loop through each task and create a row in the task list
        tasks.forEach(task => {
            const row = document.createElement('tr');
            row.innerHTML = `
                <td>${task.description}</td>
                <td>${task.start_date}</td>
                <td>${task.end_date}</td>
                <td class="actions-icons">
                    <i onclick="viewPhoto('${task.photo}')">&#128247;</i>
                    <i onclick="editTask(${task.id})">&#9998;</i>
                    <i onclick="deleteTask(${task.id})">&#128465;</i>
                    <i onclick="markAsCompleted(${task.id})">&#9989;</i>
                </td>
            `;
            taskList.appendChild(row); // Add the new row to the table
        });
    } catch (error) {
        alert('Failed to load tasks: ' + error.message); // Handle error if tasks can't be loaded
    }
}

// Function to add a new task
async function addTask() {
    const description = document.getElementById('description').value;
    const start_date = document.getElementById('start_date').value;
    const end_date = document.getElementById('end_date').value;
    const photoInput = document.getElementById('photo');
    
    if (photoInput.files.length === 0) {
        alert('Please capture a photo.'); // Ensure a photo is uploaded before adding a task
        return;
    }

    const photo = photoInput.files[0]; // Get the selected photo file
    const formData = new FormData();
    formData.append('user_id', userId);
    formData.append('pin', pin);
    formData.append('description', description);
    formData.append('start_date', start_date);
    formData.append('end_date', end_date);
    formData.append('file', photo);

    try {
        // Send a POST request to add the task
        const response = await axios.post(`${apiBaseUrl}/tasks`, formData, {
            headers: { 'Content-Type': 'multipart/form-data' }
        });
        console.log(JSON.stringify(response.data));
        alert('Task added successfully!');
        loadTasks(); // Reload the task list after adding the new task
    } catch (error) {
        alert('Failed to add task: ' + error.message); // Handle error if task can't be added
    }

    toggleForm(); // Hide the task form after adding a task
}

// Function to delete a task
async function deleteTask(taskId) {
    try {
        // Send a DELETE request to remove the task
        await axios.delete(`${apiBaseUrl}/tasks`, {
            data: { user_id: userId, pin, task_id: taskId }
        });
        alert('Task deleted successfully!');
        loadTasks(); // Reload the task list after deleting the task
    } catch (error) {
        alert('Failed to delete task: ' + error.message); // Handle error if task can't be deleted
    }
}

// Function to mark a task as completed
async function markAsCompleted(taskId) {
    try {
        // Send a PUT request to update the task's status
        await axios.put(`${apiBaseUrl}/tasks`, {
            user_id: userId,
            pin,
            task_id: taskId,
            status: 'completed'
        });
        alert('Task marked as completed!');
        loadTasks(); // Reload the task list after marking the task as completed
    } catch (error) {
        alert('Failed to mark task as completed: ' + error.message); // Handle error if task can't be marked
    }
}

// Function to view the photo of a task
function viewPhoto(photoUrl) {
    window.open(photoUrl, '_blank'); // Open the photo in a new tab
}

// Function to edit a task (currently under development)
function editTask(taskId) {
    alert('Edit functionality is under development.'); // Placeholder for edit functionality
}

// Function to toggle the visibility of the task form
function toggleForm() {
    const formSection = document.querySelector('.form-section');
    formSection.classList.toggle('active'); // Toggle the 'active' class to show or hide the form
}

// Load the tasks when the page loads
loadTasks();
```

#### Explanation:
1. API Base URL:
    * The base URL for the API is defined to interact with the backend service.
2. Loading Tasks:
    * The `loadTasks()` function retrieves tasks from the server and displays them in an HTML table. Each task has buttons to view the photo, edit it, delete it, and mark it as completed.
3. Adding a Task:
    * The `addTask()` function allows a new task to be added, including a description, start and end dates, and a photo. The photo is sent as a file attachment in the `FormData` object.
4. Deleting a Task:
    * The `deleteTask()` function removes a specific task using an HTTP DELETE request.
5. Marking a Task as Completed:
    * The `markAsCompleted()` function updates the status of a task to "completed" on the server.
6. Viewing a Task´s Photo:
    * The `viewPhoto()` function opens the photo of the task in a new window.
7. Toggle for Showing/Hiding the Form:
    * The `toggleForm()` function toggles the visibility of the task form.
8. Initial Call to Load Task:
    * The `loadTasks()` function is called when the page loads to ensure that tasks are displayed from the start.