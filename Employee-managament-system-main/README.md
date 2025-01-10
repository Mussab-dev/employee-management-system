# Employee-managament-system
Overview
The Employee Management System is a single-page application (SPA) developed using Angular 19. The project demonstrates the implementation of core Angular concepts, including routing, data binding, parent-child communication, services, dependency injection, GitHub version control, and deployment on Heroku. The system manages a list of employees stored in a local JSON file, allowing users to perform CRUD (Create, Read, Update, Delete) operations.
________________________________________
Features
1. Routing
The application implements Angular routing to navigate between different views:
•	Home: Welcome page displaying project information.
•	Employee List: Displays all employees in a tabular format.
•	Add Employee: Form to add a new employee.
•	Edit Employee: Form to edit existing employee details.
•	Employee Details: Displays detailed information of a selected employee.
2. Data Binding
•	Two-Way Data Binding: Used in forms for adding and editing employee details with [(ngModel)].
•	Property and Event Binding: Used to dynamically update the DOM and handle user interactions.
3. Parent-Child Communication
•	Input Decorator: Enables parent components to pass data to child components.
•	Output Decorator with EventEmitter: Allows child components to emit events (e.g., delete or update) to parent components.
4. Service for Data Management
An Angular service is created to:
•	Fetch employee data from a local JSON file.
•	Perform CRUD operations.
•	Use Angular's HttpClient to interact with data.
5. Dependency Injection
•	The EmployeeService is injected into components to share data and business logic.
•	Angular's dependency injection ensures a singleton service for consistent data handling across components.
6. GitHub Integration
•	The project is version-controlled using GitHub.
•	Key steps: 
o	Initialize a Git repository.
o	Commit changes after each feature addition.
o	Document the project with a README.md file.
7. Deployment on Heroku
•	The Angular app is packaged for production using ng build.
•	The app is hosted on Heroku using the Node.js buildpack.
________________________________________
Implementation Details
Project Setup
1.	Initialize Angular Project: 
2.	ng new employee-management --routing
3.	cd employee-management
4.	Create Components: 
5.	ng generate component components/home
6.	ng generate component components/employee-list
7.	ng generate component components/add-edit-employee
8.	ng generate component components/employee-details
Routing
Defined routes in app-routing.module.ts:
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'employees', component: EmployeeListComponent },
  { path: 'employees/add', component: AddEditEmployeeComponent },
  { path: 'employees/edit/:id', component: AddEditEmployeeComponent },
  { path: 'employees/:id', component: EmployeeDetailsComponent },
];
Service for Data Management
1.	Create Service: 
2.	ng generate service services/employee
3.	Service Code: 
4.	import { Injectable } from '@angular/core';
5.	import { HttpClient } from '@angular/common/http';
6.	import { Observable } from 'rxjs';
7.	
8.	@Injectable({ providedIn: 'root' })
9.	export class EmployeeService {
10.	  private url = 'assets/employee-data.json';
11.	
12.	  constructor(private http: HttpClient) {}
13.	
14.	  getEmployees(): Observable<any[]> {
15.	    return this.http.get<any[]>(this.url);
16.	  }
17.	
18.	  // Additional methods for add, edit, delete
19.	}
Parent-Child Communication
Example of communication between EmployeeListComponent and EmployeeDetailsComponent using @Input and @Output:
@Input() employee: any;
@Output() delete = new EventEmitter<number>();

onDelete(): void {
  this.delete.emit(this.employee.id);
}
Data Binding
Form example in AddEditEmployeeComponent:
<form (ngSubmit)="onSubmit()">
  <div>
    <label for="name">Name:</label>
    <input id="name" [(ngModel)]="employee.name" name="name" required />
  </div>
  <button type="submit">Save</button>
</form>
Deployment Steps
1.	Create server.js: 
2.	const express = require('express');
3.	const app = express();
4.	const path = require('path');
5.	
6.	app.use(express.static(__dirname + '/dist/employee-management'));
7.	
8.	app.get('/*', function (req, res) {
9.	  res.sendFile(path.join(__dirname + '/dist/employee-management/index.html'));
10.	});
11.	
12.	app.listen(process.env.PORT || 8080);
13.	Deploy to Heroku: 
14.	heroku login
15.	heroku create
16.	git push heroku main
________________________________________
Project Structure
JSON File (employee-data.json)
[
  {
    "id": 1,
    "name": "John Doe",
    "position": "Software Engineer",
    "department": "IT",
    "salary": 60000
  },
  {
    "id": 2,
    "name": "Jane Smith",
    "position": "Product Manager",
    "department": "Operations",
    "salary": 80000
  }
]
Components
1.	HomeComponent: Displays project information.
2.	EmployeeListComponent: Shows all employees in a table with options to view, edit, or delete.
3.	EmployeeDetailsComponent: Displays detailed information of a selected employee.
4.	AddEditEmployeeComponent: Form to add or edit an employee based on the route.

Conclusion
The Employee Management System project demonstrates the practical use of Angular's features to build a fully functional single-page application. By leveraging concepts like routing, services, and dependency injection, students gain hands-on experience in developing scalable and maintainable applications. Additionally, integrating GitHub for version control and deploying on Heroku ensures the application is production-ready.
________________________________________



