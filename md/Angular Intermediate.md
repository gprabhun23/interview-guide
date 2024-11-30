### 1. What are directives in Angular? Have you ever created a custom directive? Can you explain the steps?  
- Directives in Angular are classes that add custom behavior to elements in the DOM.  
- There are three types: Structural (`*ngIf`, `*ngFor`), Attribute (e.g., `[ngClass]`), and Component.  
- Custom directives are used to create reusable behaviors like toggling styles or handling events.  
- Steps to create a custom directive:  
  1. Use `ng generate directive <directive-name>` to scaffold the directive.  
  2. Define behavior in the `@Directive` class.  
  3. Apply the directive to elements in templates.  
- **Example**: Created a hover effect directive in a project.  
```typescript  
import { Directive, ElementRef, HostListener } from '@angular/core';  

@Directive({  
  selector: '[appHoverHighlight]'  
})  
export class HoverHighlightDirective {  
  constructor(private el: ElementRef) {}  

  @HostListener('mouseenter') onMouseEnter() {  
    this.el.nativeElement.style.backgroundColor = 'yellow';  
  }  

  @HostListener('mouseleave') onMouseLeave() {  
    this.el.nativeElement.style.backgroundColor = 'white';  
  }  
}  
```  

Applied it for dynamic hover highlighting in a dashboard component.  

---

### 2. What are the different ways to share data between components?  
- Sharing data between components depends on their relationship (parent-child, siblings, etc.).  
- Use **Input and Output** bindings for parent-child communication.  
- Use a **shared service with Subjects or BehaviorSubjects** for sibling components.  
- Use **Angular’s State Management tools** like NGRX for application-wide sharing.  
- **Example**: Used a service with BehaviorSubject for real-time updates between unrelated components in a project dashboard.  

---

### 3. Can you explain your role and responsibilities in the current project? Do you follow the Agile methodology?  
- As a full-stack developer, responsible for building Angular-based user interfaces and integrating APIs.  
- Participate in sprint planning, daily stand-ups, and retrospectives following Agile.  
- Write and optimize Angular components for scalability and performance.  
- Ensure code quality using unit tests, code reviews, and adherence to best practices.  
- **Example**: Delivered a reusable component library that reduced development time across multiple sprints.  

---

### 4. What is an Interceptor in Angular?  
- Interceptors intercept HTTP requests and responses globally in an Angular application.  
- Useful for logging, modifying headers, or handling errors.  
- Implemented by creating a class that implements `HttpInterceptor`.  
- Add the interceptor in the `providers` array using `HTTP_INTERCEPTORS`.  
- **Example**: Used an interceptor for adding authentication tokens to all API requests.  
```typescript  
import { Injectable } from '@angular/core';  
import { HttpInterceptor, HttpRequest, HttpHandler } from '@angular/common/http';  

@Injectable()  
export class AuthInterceptor implements HttpInterceptor {  
  intercept(req: HttpRequest<any>, next: HttpHandler) {  
    const authToken = 'Bearer token';  
    const authReq = req.clone({ setHeaders: { Authorization: authToken } });  
    return next.handle(authReq);  
  }  
}  
```  

---

### 5. How would you handle error handling in a centralized manner in Angular?  
- Use HTTP Interceptors for centralizing error handling.  
- Create a global error service to display error messages via UI components.  
- Use RxJS operators like `catchError` in services for more granular control.  
- Implement Angular’s `ErrorHandler` class to catch application-level errors.  
- **Example**: Centralized error handling in an e-commerce app using an interceptor to log errors and notify users.  

---

### 6. How does lazy loading work in Angular, and what are the routing guards available? How do you perform role-based routing and restrict access to certain pages in Angular?  
- Lazy loading loads feature modules only when needed to improve performance.  
- Use `loadChildren` in the route configuration to enable lazy loading.  
- Routing guards include `canActivate`, `canDeactivate`, `canLoad`, and `resolve`.  
- Implement role-based routing by checking roles in a guard and redirecting unauthorized users.  
- **Example**: Restricted admin routes by implementing a `canActivate` guard in an enterprise application.  

---

### 7. How do you manage communication between two unrelated components in Angular?  
- Use a shared service with Subject or BehaviorSubject to share data.  
- Use the Angular EventEmitter API in services for emitting events.  
- Leverage local storage or session storage for persistent data sharing.  
- Use Angular’s state management tools for global application state sharing.  
- **Example**: Built a service using BehaviorSubject for real-time notifications in unrelated dashboard widgets.  

---

### 8. How do you manage session or local storage for large data in the browser?  
- Store data in JSON format using `localStorage` or `sessionStorage`.  
- Compress data using libraries like LZ-String for large data.  
- Use IndexedDB for structured storage of large datasets.  
- Implement custom storage services for better encapsulation and reusability.  
- **Example**: Used IndexedDB for offline storage of order history in a retail app.  

---

### 9. Have you worked with Angular Material? What components have you used or customized?  
- Angular Material provides pre-built UI components that follow Material Design.  
- Frequently used components include buttons, dialogs, tables, and date pickers.  
- Customized themes using Angular Material's theming capabilities.  
- Integrated Material icons for consistent design.  
- **Example**: Customized Material tables with dynamic filtering and sorting for a data-heavy application.  

---

### 10. How does the initialization of an Angular application happen?  
- Starts with `main.ts` that bootstraps the root module (`AppModule`).  
- The root module declares components and imports modules like `BrowserModule`.  
- The `AppComponent` is the root component rendered in `index.html`.  
- Lifecycle hooks like `ngOnInit` initialize components post-bootstrap.  
- **Example**: Debugged application initialization issues using the bootstrapping sequence in `main.ts`.  

---

### 11. What are decorators in Angular?  
- Decorators are functions that add metadata to classes, methods, properties, or parameters.  
- Common decorators include `@Component`, `@Directive`, `@Injectable`, `@Input`, and `@Output`.  
- Decorators enable Angular to understand the structure and behavior of the application.  
- Used extensively for dependency injection and configuring components.  
- **Example**: Used `@Input` and `@Output` decorators for parent-child communication in reusable components.  

---

### 12. What is the importance of the ngIf directive in Angular? Can you use the ngIf directive to check if the array is empty or not?  
- `ngIf` conditionally renders DOM elements based on the given expression.  
- Improves performance by removing elements not required in the DOM.  
- Supports `else` template for fallback rendering.  
- Can check if an array is empty using `array.length`.  
- **Example**: Used `*ngIf` to show a "No Data Available" message when a table's data array was empty.  

---

### 13. Can you explain the changes in Angular 17 regarding the syntax for directives like ngFor and ngIf?  
- Angular 17 introduced simpler syntax for commonly used directives.  
- Enables compact usage of structural directives without repetition.  
- Removed some verbosity in directive implementation for improved readability.  
- Simplified examples include shorthand for conditional loops or checks.  
- **Example**: Migrated existing `*ngFor` loops to new Angular 17 syntax in a project for cleaner code.  

---

### 14. How can we communicate between components in Angular?  
- Use `@Input` for parent-to-child communication.  
- Use `@Output` with `EventEmitter` for child-to-parent communication.  
- Use a shared service for sibling or unrelated components.  
- Leverage Angular’s state management libraries for complex use cases.  
- **Example**: Used shared services for dynamic menu updates across unrelated components.  

---

### 15. What is the difference between Observable, Subject, and BehaviorSubject in Angular?  
- Observable is a data stream that emits values over time.  
- Subject is both an observer and observable; it multicasts values.  
- BehaviorSubject emits the last value upon subscription.  
- BehaviorSubject requires an initial value, unlike Subject.  
- **Example**: Used BehaviorSubject for maintaining and updating the user authentication state in a project.  

Apologies for the mix-up earlier! Let me start properly from **16** as you requested, ensuring every question is answered concisely and examples are included.  

---

### 16. What is Debounce, and why do we use it in Angular?  
- Debounce delays execution of a function after a user’s last action.  
- It reduces redundant calls, optimizing performance (e.g., during keypress events).  
- Implemented with RxJS `debounceTime` or `debounce`.  
- Used primarily in search inputs or real-time filters.  
- **Example**: Implemented `debounceTime` in a search bar to delay API calls.  
```typescript  
searchControl.valueChanges.pipe(debounceTime(300)).subscribe(query => {  
  this.searchService.search(query);  
});  
```  

---

### 17. What is the difference between hot and cold observables in Angular?  
- Cold observables emit data only when there’s an active subscription.  
- Hot observables produce data continuously, even without subscribers.  
- Cold observables are used for operations like HTTP requests.  
- Hot observables are suitable for shared event streams like WebSocket updates.  
- **Example**: Used a hot observable to stream real-time notifications in a messaging app.  

---

### 18. Why was TypeScript used in Angular (instead of JavaScript)?  
- TypeScript offers static typing, reducing runtime errors.  
- Provides powerful tooling like interfaces and decorators.  
- Supports ES6+ features, enabling modern development practices.  
- Makes the codebase more maintainable and scalable.  
- **Example**: Used TypeScript interfaces to enforce consistent API data structure validation.  

---

### 19. Do you have any questions for me?  
- What technologies are you currently exploring for future projects?  
- How does your team ensure a balance between quality and delivery timelines?  
- Can you describe the structure of the development team?  
- What are your expectations for this role in the first six months?  
- **Example**: Asked these questions in my previous interview to gauge team dynamics and project priorities.  

---

### 20. What is the difference between @HostBinding and @HostListener in Angular?  
- `@HostBinding` binds a property or attribute to the host element.  
- `@HostListener` listens to events on the host element.  
- Both are used to interact with host components or elements.  
- Commonly used in directives for DOM manipulation.  
- **Example**: Used `@HostListener` to handle clicks and `@HostBinding` to toggle classes in a hover directive.  
```typescript  
@Directive({ selector: '[appHoverHighlight]' })  
export class HoverHighlightDirective {  
  @HostBinding('class.highlight') isHighlighted = false;  
  @HostListener('mouseenter') onMouseEnter() { this.isHighlighted = true; }  
  @HostListener('mouseleave') onMouseLeave() { this.isHighlighted = false; }  
}  
```  

---

### 21. Have you ever faced event bubbling in an Angular application?  
- Event bubbling occurs when events propagate from child to parent elements.  
- Can lead to unintended consequences if not properly managed.  
- Use `stopPropagation()` to prevent bubbling.  
- Angular’s event binding automatically contains bubbling in most cases.  
- **Example**: Encountered bubbling in a nested dropdown menu and resolved it using `stopPropagation()`.  

---

### 22. Do you use Observables or Promises more frequently in Angular? Which is better for data handling?  
- Observables are more flexible than Promises for asynchronous tasks.  
- Observables can handle multiple values over time, while Promises resolve once.  
- Observables integrate seamlessly with RxJS operators like `map`, `filter`, etc.  
- Promises are simpler for one-time HTTP requests.  
- **Example**: Used Observables for real-time stock updates and Promises for user login operations.  

---

### 23. How do you unsubscribe from an Observable when navigating away from a component in Angular?  
- Use `Subscription.unsubscribe()` in the `ngOnDestroy` lifecycle hook.  
- Utilize `takeUntil` with a Subject to manage unsubscription automatically.  
- Use `async pipe` for template bindings to handle unsubscription automatically.  
- Avoid memory leaks by unsubscribing from all subscriptions.  
- **Example**: Used `takeUntil` in a dashboard component to unsubscribe from live data streams.  
```typescript  
ngOnDestroy() {  
  this.unsubscribe$.next();  
  this.unsubscribe$.complete();  
}  
```  

---

### 24. Why do we use ngOnDestroy in Angular? How do you handle async data and avoid memory leaks using ngOnDestroy?  
- `ngOnDestroy` is called when a component is destroyed.  
- Used to clean up resources like subscriptions, intervals, or listeners.  
- Unsubscribe from Observables to prevent memory leaks.  
- Clear timers or event listeners for better performance.  
- **Example**: Used `ngOnDestroy` to clear WebSocket connections in a chat application.  

---

### 25. What is the purpose of the @NgModule decorator in Angular?  
- Declares and organizes Angular modules.  
- Defines the components, directives, and pipes used within the module.  
- Specifies imports, exports, and providers for dependency injection.  
- Helps with modularization and lazy loading of features.  
- **Example**: Used `@NgModule` to structure feature modules like UserModule and AdminModule.  

---

### 26. What are the key sections inside the @NgModule decorator?  
- `declarations`: Declares components, directives, and pipes.  
- `imports`: Includes other modules like `BrowserModule` or `FormsModule`.  
- `providers`: Registers services and dependencies for DI.  
- `bootstrap`: Specifies the root component for bootstrapping.  
- **Example**: Used `imports` to integrate Angular Material in a module.  

---

### 27. Can you have multiple @NgModule decorators in an Angular application?  
- Yes, Angular supports multiple modules to modularize the application.  
- Feature modules encapsulate related functionality.  
- CoreModule contains singleton services; SharedModule contains reusable components.  
- Helps with lazy loading and reducing bundle size.  
- **Example**: Created separate modules for authentication, dashboard, and reporting in a project.  

---

### 28. How do you implement lazy loading in Angular using @NgModule?  
- Define feature modules with their own routing configurations.  
- Use `loadChildren` in the `AppRoutingModule` to load modules lazily.  
- Ensure each feature module has its own `RouterModule` configuration.  
- Improves application performance by reducing initial load size.  
- **Example**: Implemented lazy loading for an admin module in an e-commerce app.  

---

### 29. What is the purpose of the providers and declarations properties in the @NgModule decorator?  
- `providers` registers services and dependencies at the module level.  
- `declarations` registers components, directives, and pipes in the module.  
- Ensures proper DI and component recognition.  
- Prevents redeclaration errors by scoping components to their modules.  
- **Example**: Declared shared components in SharedModule and services in CoreModule.  

---

### 30. How do you add a module like the FormsModule to an Angular application?  
- Import the module in the `AppModule` or the required feature module.  
- Add the module to the `imports` array of `@NgModule`.  
- Use the directives or components provided by the module in templates.  
- Ensure proper configuration if required (e.g., ReactiveFormsModule).  
- **Example**: Used `FormsModule` for two-way binding in a user registration form.  

---

### 31. What are route guards in Angular, and how do you implement them for authentication?  
- Route guards control access to specific routes based on conditions.  
- Common types include `CanActivate`, `CanDeactivate`, and `Resolve`.  
- Implement route guards as services by extending their respective interfaces.  
- Use guards in the `AppRoutingModule` to protect routes.  
- **Example**: Used `CanActivate` guard to restrict access to admin routes for unauthorized users.  
```typescript  
@Injectable({ providedIn: 'root' })  
export class AuthGuard implements CanActivate {  
  constructor(private authService: AuthService, private router: Router) {}  
  canActivate(): boolean {  
    if (this.authService.isLoggedIn()) {  
      return true;  
    }  
    this.router.navigate(['/login']);  
    return false;  
  }  
}  
```  

---

### 32. What is the purpose of canActivate and canDeactivate route guards in Angular?  
- `CanActivate` determines whether a user can access a route.  
- `CanDeactivate` checks if a user can leave a route, useful for unsaved changes.  
- Both return boolean or Observable/Promise resolving to boolean.  
- Used to enforce authentication, permissions, or confirm actions.  
- **Example**: Used `CanDeactivate` in a form editor to prevent unsaved data loss.  

---

### 33. How do you manage data transfer between components using services and Subject in Angular?  
- Create a shared service for communication between components.  
- Use an RxJS `Subject` for broadcasting data changes.  
- Inject the service into the components needing communication.  
- Subscribe to the `Subject` to listen for updates.  
- **Example**: Used a shared service to notify components of user role changes.  
```typescript  
@Injectable({ providedIn: 'root' })  
export class DataService {  
  private userRoleSubject = new Subject<string>();  
  userRole$ = this.userRoleSubject.asObservable();  
  updateRole(role: string) {  
    this.userRoleSubject.next(role);  
  }  
}  
```  

---

### 34. How do you style components in Angular using external or inline styles?  
- External styles: Use `styleUrls` in the component metadata.  
- Inline styles: Use the `styles` property in the component metadata.  
- CSS can be scoped to components using Angular’s View Encapsulation.  
- External stylesheets can also be included globally via `angular.json`.  
- **Example**: Used `styleUrls` for maintaining reusable CSS across components.  

---

### 35. How do you apply conditional classes or styles in Angular templates?  
- Use `[class.className]` to conditionally apply a class.  
- Use `[ngClass]` for multiple dynamic classes.  
- Apply inline styles conditionally using `[style.property]` or `[ngStyle]`.  
- Useful for UI state changes like active/inactive toggles.  
- **Example**: Used `[ngClass]` to highlight selected rows in a table dynamically.  
```html  
<tr [ngClass]="{ 'selected': isSelected(row) }" *ngFor="let row of rows">  
  {{ row.name }}  
</tr>  
```  

---

### 36. How do you handle forms in Angular? (Template-driven vs. Reactive)  
- Template-driven forms rely on directives in templates and are simpler for basic forms.  
- Reactive forms provide a model-driven approach with better control and validation.  
- Use `FormsModule` for template-driven and `ReactiveFormsModule` for reactive forms.  
- Reactive forms use `FormGroup` and `FormControl` for form control management.  
- **Example**: Used reactive forms for building dynamic form fields with validation.  
```typescript  
this.form = new FormGroup({  
  name: new FormControl('', Validators.required),  
  email: new FormControl('', [Validators.required, Validators.email])  
});  
```  

---

### 37. How can you handle form validation in Angular using ReactiveForms and TemplateDrivenForms?  
- Use `Validators` for both approaches to enforce rules.  
- For reactive forms, bind errors to controls programmatically.  
- For template-driven forms, use Angular’s built-in validation directives.  
- Display error messages using conditional rendering in the template.  
- **Example**: Used reactive form validators to validate email and password fields.  

---

### 38. What are the best practices for handling dynamic content loading in Angular?  
- Use lazy loading for heavy modules or components.  
- Implement `trackBy` in `*ngFor` to optimize DOM rendering.  
- Avoid unnecessary API calls by caching data.  
- Use Angular resolvers for pre-fetching route data.  
- **Example**: Used lazy loading to defer loading of the admin dashboard module.  

---

### 39. What is the purpose of FormBuilder and FormGroup in Angular?  
- `FormBuilder` simplifies form creation using less boilerplate code.  
- `FormGroup` manages multiple form controls as a single group.  
- Use `FormBuilder` to instantiate `FormGroup` and `FormControl`.  
- Helps organize and validate complex forms easily.  
- **Example**: Used `FormBuilder` to dynamically generate a user registration form.  
```typescript  
this.form = this.fb.group({  
  username: ['', Validators.required],  
  password: ['', Validators.required]  
});  
```  

---

### 40. How can you add dynamic validation to Angular reactive form controls?  
- Use the `setValidators` method on form controls to add or update validators.  
- Use `updateValueAndValidity()` to re-evaluate validation rules.  
- Useful for conditional form requirements based on user actions.  
- Validators can be combined or removed dynamically.  
- **Example**: Added validation dynamically for a required OTP field based on user input.  

---

### 41. What is the purpose of using an interface in Angular?  
- Defines a contract for data structures to ensure type safety.  
- Simplifies API response handling by describing expected shapes.  
- Makes code more readable and maintainable.  
- Enables type-checking during development to catch errors early.  
- **Example**: Used an interface to type-check API response data for user profiles.  

---

### 42. What is the purpose of the async pipe in Angular?  
- Simplifies subscription to Observables or Promises in templates.  
- Automatically handles unsubscription to avoid memory leaks.  
- Reduces boilerplate code for manual subscription handling.  
- Useful for binding async data directly in the template.  
- **Example**: Used `async` pipe to display user notifications from an Observable stream.  
```html  
<div *ngFor="let notification of notifications$ | async">  
  {{ notification.message }}  
</div>  
```  

---

### 43. What is an Angular resolver, and how does it work?  
- Pre-fetches data for a route before navigating to it.  
- Implemented as a service using the `Resolve` interface.  
- Ensures route loads only after data is available.  
- Use `resolve` property in the `AppRoutingModule` for configuration.  
- **Example**: Used a resolver to load user details before rendering the dashboard.  

---

### 44. What is the difference between JIT and AOT compilation in Angular?  
- JIT (Just-In-Time) compiles the app in the browser at runtime.  
- AOT (Ahead-Of-Time) compiles the app during the build process.  
- AOT provides faster load times and better performance.  
- JIT is more suitable for development; AOT is recommended for production.  
- **Example**: Used AOT compilation for production builds to minimize load times.  

---

### 45. What is lazy loading in Angular, and how does it improve performance?  
- Defers loading of feature modules until they are needed.  
- Reduces the initial bundle size, improving load time.  
- Configured using `loadChildren` in routing modules.  
- Ensures efficient resource utilization and better scalability.  
- **Example**: Implemented lazy loading for the reports module in an analytics dashboard.  

---

### 46. What is the role of HTTP interceptors in Angular?  
- Intercept and modify HTTP requests or responses globally.  
- Useful for adding headers like authentication tokens to requests.  
- Can handle centralized error handling or request logging.  
- Implemented by extending the `HttpInterceptor` interface.  
- **Example**: Used an interceptor to attach JWT tokens to outgoing API calls.  
```typescript  
@Injectable()  
export class AuthInterceptor implements HttpInterceptor {  
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {  
    const cloned = req.clone({ headers: req.headers.set('Authorization', `Bearer ${token}`) });  
    return next.handle(cloned);  
  }  
}  
```  

---

### 47. What is the purpose of ViewChild and ViewChildren in Angular?  
- `ViewChild` retrieves a reference to a single DOM element or component.  
- `ViewChildren` retrieves references to multiple elements or components.  
- Access children in the component’s template for manipulation or querying.  
- Useful for DOM interactions or component communication.  
- **Example**: Used `ViewChild` to reset a child form component programmatically.  
```typescript  
@ViewChild(ChildComponent) childComp!: ChildComponent;  
resetChild() {  
  this.childComp.resetForm();  
}  
```  

---

### 48. What are entryComponents in Angular?  
- Components loaded dynamically rather than declared in a template.  
- Specified in the `entryComponents` array in earlier Angular versions.  
- No longer required in Angular 9+ due to Ivy renderer.  
- Commonly used for dialog boxes, modals, or dynamically added UI elements.  
- **Example**: Used an entry component to create a custom dynamic modal dialog.  

---

### 49. What is the role of Angular Material in an Angular application?  
- Provides pre-designed UI components for faster development.  
- Ensures consistency with Google’s Material Design guidelines.  
- Components include buttons, forms, dialogs, and tables.  
- Supports accessibility and responsiveness out of the box.  
- **Example**: Used Angular Material’s `MatTable` and `MatPaginator` for a paginated data table.  

---

### 50. What is a component in Angular?  
- A building block of Angular applications consisting of TypeScript, HTML, and CSS.  
- Defined using the `@Component` decorator.  
- Controls a specific portion of the UI and handles data binding.  
- Communicates with other components using inputs, outputs, or services.  
- **Example**: Created a reusable button component for a project.  
```typescript  
@Component({  
  selector: 'app-button',  
  template: `<button [class]="btnClass">{{ label }}</button>`  
})  
export class ButtonComponent {  
  @Input() label!: string;  
  @Input() btnClass!: string;  
}  
```  

---

### 51. How do you bind data in Angular?  
- Interpolation (`{{}}`) for binding data to templates.  
- Property binding (`[property]="expression"`) for dynamic property values.  
- Event binding (`(event)="handler"`) for listening to DOM events.  
- Two-way binding (`[(ngModel)]`) for syncing data between the UI and model.  
- **Example**: Used two-way binding to sync form input with a model.  
```html  
<input [(ngModel)]="username" placeholder="Enter your name">  
```  

---

### 52. What is ngModel, and how is it used?  
- A directive for two-way data binding in Angular.  
- Requires importing `FormsModule` in `AppModule`.  
- Binds an input element to a component property.  
- Automatically updates the property value on user input.  
- **Example**: Used `ngModel` to bind a search bar input to a component property.  

---

### 53. How do you add modules in Angular?  
- Use `ng generate module` or `ng g module` command with Angular CLI.  
- Import the module in the root or feature module.  
- Use `NgModule` metadata to configure the module’s components and services.  
- Modular architecture helps organize large applications.  
- **Example**: Added a feature module for managing user profiles in an application.  

---

### 54. What is the AppModule, and why is it important?  
- The root module of an Angular application, bootstrapped at runtime.  
- Declares and provides all components, directives, and pipes used in the app.  
- Imports essential Angular modules like `BrowserModule` and `FormsModule`.  
- Defines entry components and the root component.  
- **Example**: Configured global services and root-level declarations in `AppModule`.  

---

### 55. How do you handle routing in Angular?  
- Define routes using `RouterModule` in the `AppRoutingModule`.  
- Use `RouterOutlet` in templates to load components dynamically.  
- Link routes with `routerLink` directive.  
- Manage route parameters with `ActivatedRoute` service.  
- **Example**: Configured routes for navigation in an e-commerce application.  

---

### 56. What are the different types of Angular guards?  
- `CanActivate`: Controls access to a route.  
- `CanDeactivate`: Prevents leaving a route without confirmation.  
- `Resolve`: Pre-fetches data before route activation.  
- `CanLoad`: Restricts loading of lazy-loaded modules.  
- **Example**: Used `CanLoad` guard to restrict loading of admin modules for unauthorized users.  

---

### 57. What is the difference between a subject and an observable in Angular?  
- Observable emits data streams, while Subject emits and listens simultaneously.  
- Subjects act as both Observable and Observer.  
- Useful for multicasting data to multiple subscribers.  
- Subjects allow manual control of emitted data.  
- **Example**: Used a `Subject` in a shared service to broadcast user role changes.  

---

### 58. What is a behavior subject? How does it differ from a regular subject?  
- BehaviorSubject holds a default value and emits the latest value to new subscribers.  
- Regular Subject doesn’t retain the last emitted value.  
- Useful for managing state across components.  
- BehaviorSubject is ideal for application-level state sharing.  
- **Example**: Used BehaviorSubject to store and share authentication status.  

---

### 59. How do you handle data sharing between components in Angular?  
- Use `@Input` and `@Output` for parent-child communication.  
- Use shared services with Observables or Subjects for unrelated components.  
- Use `EventEmitter` for emitting events from child to parent.  
- Avoid tight coupling by using state management libraries for large apps.  
- **Example**: Shared user preferences using a service and BehaviorSubject.  

---

### 60. How does Angular handle data sharing between components (e.g., parent-child)?  
- Parent to child: Use `@Input` binding for passing data.  
- Child to parent: Use `@Output` and `EventEmitter`.  
- Sibling components: Use shared services with Subjects or Observables.  
- Unrelated components: Use global state management solutions like NGRX.  
- **Example**: Passed user details from parent to child using `@Input`.  

---

We have covered questions 1–60. A total of 120 questions are to be answered. This means **60 questions are pending.** Here is the next set:

---

### 61. How do you handle HTTP requests in Angular?  
- Use `HttpClient` module to send HTTP requests.  
- Provides methods like `get`, `post`, `put`, `delete` for CRUD operations.  
- Supports request options like headers, parameters, and response type.  
- Use Observables to handle asynchronous responses.  
- **Example**: Used `HttpClient` to fetch user data from a REST API.  
```typescript  
this.http.get('https://api.example.com/users').subscribe(data => console.log(data));  
```  

---

### 62. How do you work with the HttpClientModule in Angular?  
- Import `HttpClientModule` into the app or feature module.  
- Use `HttpClient` service for making HTTP calls.  
- Can intercept requests using HTTP interceptors.  
- Supports advanced features like retry logic and error handling.  
- **Example**: Imported `HttpClientModule` to enable HTTP services in `AppModule`.  

---

### 63. How do you prevent memory leaks in Angular?  
- Use `takeUntil` with a `Subject` for unsubscribing from Observables.  
- Use the `async` pipe to manage subscriptions in templates.  
- Destroy subscriptions in the `ngOnDestroy` lifecycle hook.  
- Avoid retaining unused DOM references or listeners.  
- **Example**: Used `takeUntil` to safely unsubscribe on component destruction.  
```typescript  
private destroy$ = new Subject<void>();  
this.observable.pipe(takeUntil(this.destroy$)).subscribe();  
ngOnDestroy() {  
  this.destroy$.next();  
  this.destroy$.complete();  
}  
```  

---

### 64. What is AppInitializer, and where would you use it?  
- A function or service that runs before the Angular app initializes.  
- Configured in the `providers` array of the root module.  
- Useful for preloading configurations or fetching essential data.  
- Executes during the bootstrapping process.  
- **Example**: Used AppInitializer to fetch environment settings before app loads.  

---

### 65. How do you run tests in Angular using Karma and Jasmine?  
- Write test cases using Jasmine syntax (`describe`, `it`, `expect`).  
- Use Angular CLI command `ng test` to run tests with Karma test runner.  
- Configure Karma for test execution and reporting.  
- Test both unit and integration scenarios.  
- **Example**: Wrote a unit test to verify a service function's output.  

---

### 66. What is the purpose of the angular.json file in configuring tests?  
- Configures Angular CLI build and test settings.  
- Specifies test frameworks, environments, and scripts.  
- Allows customizing Karma and Protractor configurations.  
- Defines test coverage options and output paths.  
- **Example**: Updated `angular.json` to enable detailed test coverage reports.  

---

### 67. How do you generate a coverage report in Angular tests?  
- Run tests using `ng test --code-coverage` command.  
- Generates a `coverage` folder in the root directory.  
- Open `index.html` inside the folder to view detailed coverage.  
- Includes metrics like lines, branches, and functions covered.  
- **Example**: Used coverage reports to optimize under-tested components.  

---

### 68. How do you debug an Angular application?  
- Use Chrome Developer Tools to inspect elements and console logs.  
- Use Angular DevTools for component and state debugging.  
- Add breakpoints in TypeScript files using source maps.  
- Leverage `console.log` and debugging utilities for real-time insights.  
- **Example**: Debugged a routing issue by analyzing the navigation state in Angular DevTools.  

---

### 69. How do you mock services for testing in Angular?  
- Create mock classes that implement the service interface.  
- Use `TestBed` to provide mock services during tests.  
- Replace actual dependencies with mock versions using `useClass` or `useValue`.  
- Test component behavior independently of service logic.  
- **Example**: Mocked an API call by returning a predefined response.  
```typescript  
const mockService = { getData: () => of([{ id: 1, name: 'Test' }]) };  
```  

---

### 70. What is the difference between unit testing and integration testing?  
- Unit testing focuses on individual components or functions in isolation.  
- Integration testing validates interactions between components or modules.  
- Unit tests are faster and easier to debug.  
- Integration tests ensure overall system correctness.  
- **Example**: Used unit testing to validate form validation logic in a component.  

---

### 71. How do you structure an Angular project for scalability?  
- Use feature modules to group related functionality.  
- Separate shared modules for reusable components and services.  
- Use consistent naming conventions for files and folders.  
- Modularize services, pipes, and directives.  
- **Example**: Organized e-commerce features like product listing and cart into feature modules.  

---

### 72. How do you break down an e-commerce website into modules and components?  
- Create feature modules like `Product`, `Cart`, `Order`, and `User`.  
- Use components for UI elements like product cards, filters, and headers.  
- Define shared services for managing cart data and API interactions.  
- Create reusable components for common features like modals.  
- **Example**: Built a `ProductCard` component and reused it across the site.  

---

### 73. How do you manage shared components in an Angular project?  
- Create a shared module to declare and export reusable components.  
- Import the shared module in feature modules where needed.  
- Avoid duplicating components by centralizing their definitions.  
- Update the shared module to include additional components or pipes.  
- **Example**: Added a custom `LoadingSpinner` component to a shared module.  

---

### 74. What is role-based access control (RBAC), and how do you implement it in Angular?  
- RBAC restricts user actions based on assigned roles.  
- Implement using route guards and conditional UI rendering.  
- Store roles in JWT tokens or a user management service.  
- Validate roles during route navigation or API calls.  
- **Example**: Used `canActivate` guard to block unauthorized users from admin routes.  

---

### 75. What is Clean Architecture? How do you implement it in Angular?  
- A layered design approach separating concerns like UI, business logic, and data access.  
- Use feature modules for UI and core modules for shared services.  
- Ensure that dependencies flow inward, not outward.  
- Utilize interfaces for dependency inversion.  
- **Example**: Structured an Angular application using clean architecture for maintainability.  

---

### 76. How do you deploy an Angular application?  
- Use `ng build --prod` to generate production-ready static files.  
- Deploy files to a web server like Apache, Nginx, or Azure Static Web Apps.  
- Configure routing with `rewrites` or `.htaccess` for SPA navigation.  
- Use CI/CD pipelines for automated deployment.  
- **Example**: Deployed the application to AWS S3 with CloudFront for faster delivery.  

---

### 77. What is the difference between ng build and ng serve?  
- `ng build` compiles the app into static files for deployment.  
- `ng serve` runs a development server for local testing.  
- `ng build` includes optimizations like AOT and minification for production builds.  
- `ng serve` provides live reloading for development.  
- **Example**: Used `ng build` to generate a production version before deploying.  

---

### 78. How do you configure multiple environments in Angular?  
- Define environment-specific files like `environment.prod.ts` and `environment.dev.ts`.  
- Use the `fileReplacements` option in `angular.json` to switch environments.  
- Access environment variables via the `environment` object.  
- Build the application using flags like `--configuration=production`.  
- **Example**: Configured `API_BASE_URL` for different environments in the app.  

---

### 79. How do you manage dependencies and versions in an Angular project?  
- Use `package.json` to declare project dependencies.  
- Use `npm` or `yarn` to install and manage dependencies.  
- Lock dependency versions with `package-lock.json` or `yarn.lock`.  
- Update dependencies periodically using tools like `npm-check-updates`.  
- **Example**: Resolved version conflicts by updating all related packages.  

---

### 80. What happens when you run npm install?  
- Downloads and installs packages listed in `package.json`.  
- Resolves dependencies and creates `node_modules`.  
- Updates `package-lock.json` to lock specific versions.  
- Installs both development and production dependencies.  
- **Example**: Installed required packages for Angular Material using `npm install`.  

---

### 81. What is the purpose of the package-lock.json file?  
- Locks exact dependency versions to ensure consistency across environments.  
- Provides a snapshot of the dependency tree.  
- Speeds up future installations by caching resolved packages.  
- Helps in debugging version conflicts.  
- **Example**: Used `package-lock.json` to restore the exact dependency tree on a new system.  

---

### 82. How do you handle node version conflicts?  
- Use a version manager like `nvm` to switch between Node versions.  
- Specify the required version in a `.nvmrc` file.  
- Update Node.js to compatible versions when required.  
- Test the application on multiple versions during development.  
- **Example**: Resolved compatibility issues by switching to Node.js LTS version.  

---

### 83. How do you use the --force flag in npm?  
- Forces installation of packages despite errors or warnings.  
- Used to bypass peer dependency conflicts.  
- Risky as it might lead to compatibility issues.  
- Use sparingly and test thoroughly after using it.  
- **Example**: Installed a specific library version by using `npm install package-name --force`.  

---

### 84. How do you manage state in an Angular application?  
- Use services to share and manage state across components.  
- Employ state management libraries like NgRx or Akita for complex applications.  
- Use `BehaviorSubject` or `ReplaySubject` for reactive state updates.  
- Keep the application state immutable wherever possible.  
- **Example**: Used NgRx for managing the shopping cart state in an e-commerce app.  

---

### 85. What does the Angular CLI do when you add a component to your project?  
- Creates a new component file structure (HTML, TS, CSS, spec).  
- Updates `AppModule` or feature module with the new component.  
- Automatically adds component dependencies if routing is enabled.  
- Provides configuration flags for customization during creation.  
- **Example**: Used `ng generate component header` to add a header component with routing.  

---

### 86. What is the difference between Angular CLI commands like ng build, ng serve, and ng test?  
- `ng build`: Compiles app into static files for deployment.  
- `ng serve`: Starts a development server with live reload.  
- `ng test`: Runs unit tests using Karma and Jasmine.  
- `ng build` focuses on production readiness; `ng serve` is for local testing.  
- **Example**: Used `ng test` to validate a new service implementation.  

---

### 87. How do you handle custom pipes in Angular?  
- Create a pipe class using the `@Pipe` decorator.  
- Implement the `PipeTransform` interface to define transformation logic.  
- Register the pipe in the module's `declarations` array.  
- Use the pipe in templates with the `|` operator.  
- **Example**: Created a `CurrencyFormatterPipe` to display formatted prices.  
```typescript  
@Pipe({ name: 'currencyFormatter' })  
export class CurrencyFormatterPipe implements PipeTransform {  
  transform(value: number): string {  
    return `$${value.toFixed(2)}`;  
  }  
}  
```  

---

### 88. What are content projection and ng-content slots?  
- Content projection allows inserting custom content into a component template.  
- Use the `<ng-content>` tag to define projection slots.  
- Supports single or multiple slots with `select` attributes.  
- Enhances component reusability and flexibility.  
- **Example**: Used `ng-content` for creating a reusable card component.  

---

### 89. What is NGRX, and how do you use it for state management in Angular?  
- A Redux-inspired state management library for Angular.  
- Stores application state in a centralized store.  
- Manages state changes through actions, reducers, and effects.  
- Ensures a predictable state flow across the application.  
- **Example**: Used NGRX to manage user authentication state in a dashboard app.  

---

### 90. How do you handle side effects in NGRX using effects?  
- Use `@ngrx/effects` to handle asynchronous tasks like HTTP requests.  
- Define effects as Observables that listen to actions and trigger side effects.  
- Use `Actions` stream to map actions to effects.  
- Dispatch new actions based on the effect's outcome.  
- **Example**: Created an effect to fetch products from an API when the app loads.  

---

### 91. Can you explain the difference between a smart component and a dumb component in Angular?  
- Smart components manage logic and data; dumb components focus on presentation.  
- Smart components communicate with services or APIs; dumb components rely on inputs/outputs.  
- Smart components handle state changes; dumb components only receive data.  
- Dumb components are reusable and focused on UI.  
- **Example**: Created a smart component for fetching and storing user data and a dumb component for displaying it.  

---

### 92. How would you handle data sharing between components in Angular?  
- Use `@Input()` and `@Output()` for parent-child communication.  
- Use services with observables for sibling and parent-child communication.  
- Employ state management libraries like NgRx for global state sharing.  
- Use `EventEmitter` to send data from child to parent.  
- **Example**: Used a shared service with `BehaviorSubject` to manage theme preferences across components.  

---

### 93. Can you explain dependency injection in Angular and how it works?  
- Angular uses dependency injection (DI) to provide services and dependencies.  
- DI simplifies the creation and management of services across components.  
- Services are injected through constructors or `@Injectable` decorators.  
- DI helps in improving modularity and testability.  
- **Example**: Injected an authentication service into a component to manage user login.  
```typescript  
constructor(private authService: AuthService) {}  
```

---

### 94. What is the purpose of HostBinding and HostListener decorators in Angular?  
- `@HostBinding` binds properties or attributes to the host element.  
- `@HostListener` listens for events on the host element.  
- These decorators are used for enhancing the behavior of components without modifying templates.  
- They are useful for working with DOM events directly within the component.  
- **Example**: Used `@HostListener` to detect mouse events and `@HostBinding` to change class based on the event.  
```typescript  
@HostBinding('class.active') isActive = false;  
@HostListener('mouseenter') onMouseEnter() {  
  this.isActive = true;  
}  
```

---

### 95. Can you explain how an Angular Interceptor works and how you can add it to an Angular application?  
- An HTTP interceptor intercepts and modifies HTTP requests or responses.  
- It allows for tasks like adding authentication headers or logging.  
- Interceptors are added to the `HTTP_INTERCEPTORS` array in the providers section.  
- They can modify outgoing requests and incoming responses globally.  
- **Example**: Used an interceptor to add an authentication token to HTTP requests.  
```typescript  
@Injectable()  
export class AuthInterceptor implements HttpInterceptor {  
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {  
    const clonedRequest = req.clone({  
      setHeaders: { Authorization: `Bearer ${this.authService.getToken()}` }  
    });  
    return next.handle(clonedRequest);  
  }  
}  
```

---

### 96. What changes were introduced in Angular 16 and 17 regarding modules and component creation?  
- Angular 16 introduced standalone components to reduce module reliance.  
- Standalone components eliminate the need for `@NgModule` in certain cases.  
- Angular 17 further enhanced support for reactive forms and directive bindings.  
- These changes aim to simplify application structure and improve modularity.  
- **Example**: Migrated components to be standalone in Angular 16 for improved readability and testability.  

---

### 97. What is npm in the context of Angular? Why is it important?  
- `npm` (Node Package Manager) is a package manager for JavaScript.  
- It is used to install and manage libraries and dependencies in an Angular project.  
- `npm` ensures that the correct versions of libraries are installed.  
- It is essential for managing dependencies and scripts in an Angular app.  
- **Example**: Used `npm install` to add Angular Material to my project for UI components.  

---

### 98. What is the significance of the @angular/core module in Angular applications?  
- `@angular/core` contains essential Angular features like components, directives, services, and dependency injection.  
- It includes foundational decorators like `@Component`, `@NgModule`, and `@Injectable`.  
- The module provides APIs for core functionality, like lifecycle hooks and change detection.  
- It is a mandatory module for every Angular application.  
- **Example**: Imported `@angular/core` in my custom service to use the `@Injectable()` decorator.  

---

### 99. How do you handle routing in Angular?  
- Use `RouterModule` to define routes in the application.  
- Define routes in an array and configure them in the module's imports section.  
- Use `routerLink` for navigation and `ActivatedRoute` for route parameters.  
- Implement lazy loading for better performance with feature modules.  
- **Example**: Configured routing for an admin and user module in the application.  
```typescript  
const routes: Routes = [  
  { path: 'admin', loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule) }  
];  
```

---

### 100. What are the different types of Angular guards (canActivate, canDeactivate)?  
- `canActivate`: Checks if a route can be activated.  
- `canDeactivate`: Ensures a user can leave the current route.  
- `canLoad`: Prevents loading a module based on conditions.  
- `resolve`: Pre-fetches data before a route is activated.  
- **Example**: Implemented `canActivate` guard to prevent unauthorized users from accessing certain pages.  
```typescript  
canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {  
  return this.authService.isLoggedIn();  
}
```

---

There are **10 questions** pending. Here's the next set:

---

### 101. What is the difference between Observable, Subject, and BehaviorSubject in Angular?  
- **Observable**: Streams of data that you can subscribe to.  
- **Subject**: A type of Observable that allows multicasting to many Observers.  
- **BehaviorSubject**: A Subject that holds a current value and emits it to new subscribers.  
- **Observable** is used for one-time data streams; **BehaviorSubject** is used for streams with a starting value.  
- **Example**: Used a `BehaviorSubject` to store and emit the current user's authentication state.  
```typescript  
private userSubject = new BehaviorSubject<User>(null);  
currentUser$ = this.userSubject.asObservable();  
```

---

### 102. What is Debounce and why do we use it in Angular?  
- **Debounce**: Delays the processing of an event until a specified amount of time has passed.  
- Used to avoid unnecessary API calls or heavy computations on every user input.  
- Commonly used with search inputs to wait for the user to stop typing before sending a request.  
- It prevents high frequency, redundant API calls.  
- **Example**: Used debounce in a search bar to wait for the user to stop typing before making an API call.  
```typescript  
searchTerm = new Subject<string>();  
this.searchTerm.pipe(debounceTime(300), switchMap(query => this.searchService.search(query)))  
  .subscribe(results => this.searchResults = results);  
```

---

### 103. What is the difference between hot and cold observables in Angular?  
- **Cold Observable**: Starts emitting values only when subscribed to, e.g., HTTP requests.  
- **Hot Observable**: Emits values immediately and shares them with all subscribers, e.g., event streams.  
- Cold observables can result in multiple calls to the server if subscribed multiple times.  
- Hot observables are shared, so the same event is emitted to all subscribers.  
- **Example**: Used a cold observable for an HTTP request and a hot observable for a WebSocket connection.  

---

### 104. Why was TypeScript used in Angular (instead of JavaScript)?  
- TypeScript offers static typing, which helps catch errors early.  
- Provides better tooling support with IntelliSense, refactoring, and auto-completion.  
- Improves code maintainability and readability with features like classes, interfaces, and decorators.  
- TypeScript's strict typing ensures more reliable code for large applications.  
- **Example**: Used TypeScript’s strong typing to define strict interfaces for API response objects, reducing runtime errors.  

---

### 105. Do you have any questions for me?  
- This question is asked in interviews to gauge your interest and understanding of the role.  
- Ask about the team structure, project technologies, or challenges the company faces.  
- Inquire about how they measure success or what a typical day looks like.  
- Show interest in their approach to software development or their adoption of new technologies.  
- **Example**: "Can you share more about the team's approach to implementing Angular best practices?"  

---

### 106. What is the difference between @HostBinding and @HostListener in Angular?  
- **@HostBinding** binds properties or attributes to the host element of a directive or component.  
- **@HostListener** listens to events on the host element.  
- `@HostBinding` is used to manipulate DOM properties, while `@HostListener` is used for event handling.  
- Both decorators enhance the interaction with the host element, but for different purposes.  
- **Example**: Used `@HostListener` to detect mouse events and `@HostBinding` to apply styles dynamically.  
```typescript  
@HostListener('mouseenter') onMouseEnter() {  
  this.isHovered = true;  
}  
@HostBinding('style.backgroundColor') get backgroundColor() {  
  return this.isHovered ? 'blue' : 'gray';  
}
```

---

### 107. Have you ever faced event bubbling in an Angular application?  
- Event bubbling occurs when an event triggered on a child element propagates to its parent elements.  
- It can lead to unintended actions if not managed properly.  
- Prevent bubbling using `event.stopPropagation()` or `event.preventDefault()`.  
- In Angular, event bubbling can be handled with `@HostListener` and `@Output`.  
- **Example**: Stopped the bubbling of a click event in a child component to prevent the parent’s click handler from triggering.  
```typescript  
@HostListener('click', ['$event']) onClick(event: MouseEvent) {  
  event.stopPropagation();  
}
```

---

### 108. Do you use Observables or Promises more frequently in Angular? Which is better for data handling?  
- **Observables** are more flexible, support multiple values, and can be cancelled or unsubscribed.  
- **Promises** are simpler and resolve a single value once.  
- Observables are better suited for continuous streams like HTTP requests, user events, etc.  
- Promises are ideal for handling single asynchronous results.  
- **Example**: Used Observables for handling HTTP requests, and Promises for handling single async results in a form validation scenario.  

---

### 109. How do you unsubscribe from an Observable when navigating away from a component in Angular?  
- Use the `ngOnDestroy` lifecycle hook to unsubscribe from Observables.  
- It ensures that subscriptions do not persist after the component is destroyed, preventing memory leaks.  
- You can store subscriptions in an array and unsubscribe them in `ngOnDestroy`.  
- Another approach is using the `takeUntil` operator to automatically unsubscribe.  
- **Example**: Unsubscribed from an Observable in the `ngOnDestroy` lifecycle hook.  
```typescript  
ngOnDestroy() {  
  this.subscription.unsubscribe();  
}
```

---

### 110. Why do we use ngOnDestroy in Angular? How do you handle async data and avoid memory leaks using ngOnDestroy in Angular?  
- `ngOnDestroy` is used to clean up resources, cancel subscriptions, and remove event listeners when a component is destroyed.  
- It helps in preventing memory leaks by ensuring subscriptions and other resources are disposed of.  
- For async data, unsubscribe from Observables in `ngOnDestroy` or use the `takeUntil` operator.  
- It is important for managing resources and cleaning up timers, subscriptions, etc.  
- **Example**: Used `ngOnDestroy` to unsubscribe from a timer Observable to avoid memory leaks.  
```typescript  
ngOnDestroy() {  
  this.timerSubscription.unsubscribe();  
}
```

---
