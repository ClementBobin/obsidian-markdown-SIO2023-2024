# File for language coding
## HTML (.html)

- **Purpose**: [HTML](HTML.md) (HyperText Markup Language) files are used to create the structure and content of web pages. They define the layout, headings, paragraphs, images, links, forms, and other elements that make up a webpage.
    
- **Example**:
    

```html
<!DOCTYPE html> 
<html> 
	<head>     
		<title>My Webpage</title> 
	</head> 
	<body>     
		<h1>Hello, World!</h1>     
		<p>This is an example of an HTML file.</p>     
		<img src="image.jpg" alt="An example image">     
		<a href="https://www.example.com">Visit Example Website</a> 
	</body> 
</html>
```

## CSS (.css)

- **Purpose**: [CSS](Css.md) (Cascading Style Sheets) files are used to control the presentation and layout of HTML documents. They define the styles, such as colors, fonts, margins, and positions, to make web pages visually appealing and responsive.
    
- **Example**:
    

```css
/* style.css */  
body {     
	font-family: Arial, sans-serif;     
	background-color: #f0f0f0; 
}  

h1 {     
	color: blue; 
}  

p {     
	font-size: 16px;     
	line-height: 1.5; 
}  

img {     
	width: 100%;     
	max-width: 500px;     
	display: block;     
	margin: 0 auto; 
}  

a {     
	color: green;     
	text-decoration: none; 
}
```

## JavaScript (.js)

- **Purpose**: [JavaScript](Javascript.md) files are used to add interactivity and dynamic behavior to web pages. They enable client-side scripting, allowing developers to manipulate the DOM (Document Object Model), handle events, and perform various actions based on user interactions.
    
- **Example**:
    

```js
// script.js  
function showMessage() {     
	const name = prompt('What is your name?');     
	alert(`Hello, ${name}! Welcome to our website.`); 
}  

document.querySelector('#greetButton').addEventListener('click', showMessage);
```

```html
<!-- index.html -->  
<!DOCTYPE html> 
<html> 
	<head>     
		<title>My Webpage</title> 
	</head> 
	<body>     
		<h1>Hello, World!</h1>     
		<button id="greetButton">Click to Greet</button>      
		<script src="script.js"></script> 
	</body> 
</html>
```

## .env

- **Purpose**: .env files are used to store environment variables for a project. These variables can include configuration settings, API keys, database credentials, and other sensitive information. They help keep sensitive data separate from the codebase and allow for easy configuration across different environments (e.g., development, staging, production).
    
- **Example**:
    

```env
DATABASE_URL=postgres://username:password@localhost:5432/mydatabase 
API_KEY=your_api_key_here 
SECRET_KEY=my_secret_key
```

## Package.json

- **Purpose**: The package.json file is a manifest for Node.js projects. It contains metadata about the project, such as its name, version, dependencies, scripts, and other information required for package management and project setup.
    
- **Example**:
    

```json
{     
	"name": "my-app",     
	"version": "1.0.0",     
	"description": "My web application",     
	"main": "index.js",     
	"scripts": {         
		"start": "node index.js",         
		"test": "jest"     
	},     
	"dependencies": {         
		"express": "^4.17.1",         
		"axios": "^0.21.1"     
	},     
	"devDependencies": {         
		"jest": "^27.0.4"     
	} 
}
```

## .gitignore

- **Purpose**: The .gitignore file specifies which files and directories should be ignored by version control systems like Git. It allows developers to exclude unnecessary or sensitive files from being committed to the repository, preventing them from being tracked and shared with others.
    
- **Example**:
    

```gitignore
node_modules/ dist/ .env
```

## README.md

- **Purpose**: The [README.md](markdown.md) file serves as documentation for the project. It provides essential information about the project's purpose, installation instructions, usage, and other relevant details for users and contributors.
    
- **Example**:
    

```md
# My Web Application  
This is a web application built with HTML, CSS, and JavaScript.  

## Installation  
1. Clone the repository. 
2. Install the dependencies: `npm install`. 
3. Start the server: `npm start`.  

## Usage  
Open `index.html` in your web browser to use the application.  

## License  
MIT License
```

## .htaccess

- **Purpose**: The .htaccess file is used on Apache web servers to control server configuration and behavior. It can be used to set rules for URL rewriting, enable compression, manage redirects, and enhance security.
    
- **Example**:
    

```htaccess
RewriteEngine On 
RewriteRule ^old-page$ /new-page [R=301,L]
```

## JSON (.json)

- **Purpose**: JSON (JavaScript Object Notation) files are used to store and exchange data in a lightweight, human-readable format. They are commonly used for configuration files, API responses, and data interchange between client and server.
    
- **Example**:
    

```json
{     
	"name": "John Doe",     
	"age": 30,     
	"email": "john@example.com" 
}
```

## .scss, .less

- **Purpose**: SCSS (Sass) and LESS files are preprocessor files for CSS. They allow developers to use variables, nested rules, and other advanced features not available in standard CSS, making stylesheets more maintainable and organized.
    
- **Example** (SCSS):
    

```scss
// style.scss  
$primary-color: #007bff;  
body {     
	font-family: Arial, sans-serif;     
	background-color: #f0f0f0; 
} 

h1 {     
	color: $primary-color; 
}
```

## .yaml, .yml

- **Purpose**: YAML (YAML Ain't Markup Language) files are used for data serialization and configuration. They are human-readable and often used in configuration files for applications.
    
- **Example**:
    

```yaml
# config.yml  
database:   
	host: localhost   
	port: 5432   
	username: user123   
	password: secret123
```

## .sql

- **Purpose**: [SQL](databases/mariadb) (Structured Query Language) files are used to define and manipulate databases. They contain SQL commands to create tables, insert data, query data, and perform other database operations.
    
- **Example**:
    

```sql
-- create_table.sql  
CREATE TABLE users (     
	id SERIAL PRIMARY KEY,     
	name VARCHAR(50) NOT NULL,     
	email VARCHAR(100) NOT NULL 
);
```

## .jsx

- **Purpose**: .jsx files are used in [React](React.md) projects for writing React components using JSX (JavaScript XML) syntax. JSX allows developers to write HTML-like code within JavaScript, making it easier to create and manage component-based user interfaces.
    
- **Example**:
    

```jsx
// App.jsx  
import React from 'react';  

function App() {     
	return (         
		<div>             
			<h1>Hello, React!</h1>             
			<p>This is a JSX file.</p>         
		</div>     
	); 
}  

export default App;
```

## .cjs

- **Purpose**: .cjs (CommonJS) files are used in Node.js projects for implementing modules using CommonJS module system. CommonJS is the module format used in Node.js for exporting and importing modules.
    
- **Example**:
    

```js
// module.cjs  
const add = (a, b) => a + b; 
module.exports = add;
```

## .bin

- **Purpose**: .bin files are binary executable files. They contain compiled machine code and are used to execute specific tasks or applications.
    
- **Example**: Binary files don't have a human-readable example, as they are not intended to be edited directly by developers.
    

## .gltf

- **Purpose**: .gltf (GL Transmission Format) files are used for 3D models and scenes. They store 3D model data, including geometry, textures, materials, animations, and more.
    
- **Example**: .gltf files contain binary data and are not human-readable. They are typically exported from 3D modeling software or generated by tools.
    

## .txt

- **Purpose**: .txt files are plain text files used for storing unformatted text data. They are simple and versatile, often used for storing configuration, logs, notes, or any text-based content.
    
- **Example**:
    

```txt
This is a text file. It contains plain text data without any special formatting.
```

## .map

- **Purpose**: .map files are source map files used for debugging and mapping minified or transpiled code back to its original source code. They help developers debug and trace errors in production code.
    
- **Example**: .map files contain mappings and are not intended for direct human editing.
    

## .ts

- **Purpose**: .ts (TypeScript) files are used in TypeScript projects. TypeScript is a superset of JavaScript that adds static typing and other features to enhance JavaScript development.
    
- **Example**:
    

```ts
// greeter.ts  
function greet(name: string) {     
	return `Hello, ${name}!`; 
}  

console.log(greet('John'));
```

## .php

- **Purpose**: .php files are used in [PHP](Php.md) projects for server-side scripting. PHP is a popular server-side programming language that is embedded within HTML files to create dynamic web pages and interact with databases.
    
- **Example**:
    

```php
// index.php  
<!DOCTYPE html> 
<html> 
	<head>     
		<title>PHP Example</title> 
	</head> 
	<body>     
		<?php     
			$name = "John";     
			echo "<h1>Hello, $name!</h1>";     
		?> 
	</body> 
</html>
```

In the above example, the PHP code between `<?php` and `?>` tags is executed on the server-side, and the value of `$name` is dynamically inserted into the HTML output.

# File divers

## BMP (fichier d'image non compressé)
https://fr.wikipedia.org/wiki/Windows_bitmap

## Conclusion

Different types of files serve various purposes in web development and software projects. Understanding their roles and usage is essential for effective project management, collaboration, and maintaining a clean and organized codebase. Happy coding and organizing your projects!
