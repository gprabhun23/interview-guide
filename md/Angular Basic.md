1. **What lifecycle hook should you use when accessing a child component using @ViewChild?**
   - Use `ngAfterViewInit` for accessing child components via `@ViewChild`.
   - `ngAfterViewInit` ensures the child component is fully initialized.
   - It’s important because `ngOnInit` is too early to access the child components.
   - The `ngAfterViewInit` hook runs after Angular initializes the component’s views.
   - Example:  
     ```typescript
     @ViewChild(ChildComponent) child: ChildComponent;
     ngAfterViewInit() {
         this.child.someMethod();
     }
     ```

2. **Have you worked with Angular Material? Can you explain how to open a dialog using Angular Material?**
   - Angular Material provides a `MatDialog` service to manage dialog windows.
   - You need to inject `MatDialog` in the constructor of your component.
   - Use `open()` method of `MatDialog` to open the dialog.
   - Dialogs can be customized with a component or template.
   - Example:  
     ```typescript
     import { MatDialog } from '@angular/material/dialog';
     constructor(private dialog: MatDialog) {}

     openDialog() {
         this.dialog.open(DialogComponent, { data: { message: 'Hello' } });
     }
     ```

3. **How can you pass data to a dialog in Angular Material?**
   - Data can be passed using the `data` property in the `open()` method.
   - This data will be accessible in the dialog component through `MAT_DIALOG_DATA`.
   - The data is passed as an object.
   - The `DialogComponent` can inject the data in its constructor.
   - Example:  
     ```typescript
     import { MAT_DIALOG_DATA } from '@angular/material/dialog';

     constructor(@Inject(MAT_DIALOG_DATA) public data: any) {}
     ```

4. **What is the use of ngOnChanges lifecycle hook in Angular? Can you provide an example where it is used?**
   - `ngOnChanges` is used to detect changes to input properties (`@Input()`).
   - It is triggered whenever the value of an `@Input()` property changes.
   - This hook provides both the current and previous values of the input.
   - Useful for reacting to changes in input data and performing actions like recalculating values.
   - Example:  
     ```typescript
     @Input() item: string;
     ngOnChanges(changes: SimpleChanges) {
         console.log('Previous value: ', changes['item'].previousValue);
         console.log('Current value: ', changes['item'].currentValue);
     }
     ```

5. **How do you compare form values (e.g., password and confirm password) in Angular forms?**
   - You can use a custom validator to compare form values like password and confirm password.
   - This is typically done in the form group’s `validator` property.
   - The validator checks whether both fields match.
   - It's helpful in ensuring the password fields are identical before submission.
   - Example:  
     ```typescript
     import { AbstractControl, ValidationErrors } from '@angular/forms';

     export function confirmPasswordValidator(control: AbstractControl): ValidationErrors | null {
         const password = control.get('password');
         const confirmPassword = control.get('confirmPassword');
         if (password && confirmPassword && password.value !== confirmPassword.value) {
             return { passwordsNotMatching: true };
         }
         return null;
     }
     ```

6. **What are the differences between eager loading and lazy loading in Angular?**
   - Eager loading loads all modules at the application startup.
   - Lazy loading loads modules only when they are needed, improving initial load time.
   - Eager loading is simpler to implement but may lead to slower performance in large apps.
   - Lazy loading is more efficient for large applications and better for performance optimization.
   - Example:  
     ```typescript
     const routes: Routes = [
         { path: 'home', component: HomeComponent },
         { path: 'about', loadChildren: () => import('./about/about.module').then(m => m.AboutModule) }
     ];
     ```

7. **What are Angular Standalone components, and how are they different from the traditional module-based components?**
   - Standalone components don’t require a module for declarations or imports.
   - They simplify the structure of Angular apps by eliminating the need for a separate module.
   - You can use them directly in routes or other components.
   - Standalone components can be used independently or with other standalone components.
   - Example:  
     ```typescript
     @Component({
         selector: 'app-standalone',
         standalone: true,
         imports: [CommonModule],
         template: `<div>Standalone Component</div>`
     })
     export class StandaloneComponent {}
     ```

8. **What are standalone components in Angular 16/17, and how does the application structure? Why are they considered a best practice in Angular 16+?**
   - Standalone components reduce the complexity of modules by allowing components to exist independently.
   - They encourage modularity and make applications more maintainable and scalable.
   - They simplify the routing process and can be directly used in routes or other components.
   - Angular 16+ promotes their use for better encapsulation and easier testing.
   - Example:  
     ```typescript
     @Component({
         selector: 'app-feature',
         standalone: true,
         imports: [CommonModule],
         template: `<h1>Feature Component</h1>`
     })
     export class FeatureComponent {}
     ```

9. **How do you manage routing and components in a project when using Angular versions that don't use modules (standalone components)?**
   - In Angular 16+, routes can be defined using the `imports` property of the `@Component` decorator.
   - Routing can directly reference standalone components without needing to wrap them in modules.
   - Lazy loading and child routes work seamlessly with standalone components.
   - Each component can be imported directly into the routing configuration.
   - Example:  
     ```typescript
     const routes: Routes = [
         { path: 'home', component: HomeComponent },
         { path: 'about', component: AboutComponent }
     ];
     ```

10. **How does Angular 16 make it easier to maintain a project with Standalone Components?**
    - Standalone components reduce the overhead of maintaining multiple modules.
    - Angular 16+ introduces better encapsulation and dependency management within components.
    - The routing system is simplified by directly referencing components, removing the need for intermediary modules.
    - They improve the modularity of the application, allowing more reusable components.
    - Example:  
      ```typescript
      @Component({
          selector: 'app-module-less',
          standalone: true,
          imports: [CommonModule],
          template: `<div>Module-less Component</div>`
      })
      export class ModuleLessComponent {}
      ```

11. **What is Angular Signals? How does it improve the framework's reactivity? Purpose of signals?**
    - Angular Signals is a reactive system introduced in Angular 16 for better reactivity management.
    - It helps manage state and updates more efficiently, without needing extensive observables.
    - Signals optimize the change detection mechanism, reducing unnecessary checks.
    - They simplify state management, especially in reactive forms and dynamic data-driven applications.
    - Example:  
      ```typescript
      import { signal } from '@angular/core';

      const count = signal(0);
      count.update(value => value + 1);
      ```

12. **How would you structure an Angular project? What components would you place in the core, shared, and feature modules?**
    - **Core Module**: Singleton services, guards, interceptors, and application-wide components.
    - **Shared Module**: Reusable components, directives, and pipes that can be used across multiple feature modules.
    - **Feature Module**: Group related components, services, and routes specific to a feature.
    - Example:  
      ```typescript
      @NgModule({
          declarations: [HeaderComponent, FooterComponent],
          exports: [HeaderComponent, FooterComponent],
          imports: [CommonModule]
      })
      export class SharedModule {}
      ```

13. **How do you manage dependencies in a large Angular application?**
    - Use Angular modules to organize dependencies and services.
    - Group related services and components into feature modules to reduce dependencies between unrelated parts of the app.
    - Lazy load modules to only load what’s necessary, reducing initial load time.
    - Use `providedIn: 'root'` for global services to avoid redundancy.
    - Example:  
      ```typescript
      @Injectable({
          providedIn: 'root'
      })
      export class UserService {}
      ```

14. **Have you used ngFor in Angular? Are you familiar with the updated syntax in recent Angular versions? How do you use ngFor to apply styles to even and odd rows?**
    - `ngFor` is used to loop over arrays or objects to display a list of items.
    - In recent versions, `ngFor` can be enhanced with `trackBy` for performance optimization.
    - To apply styles to even and odd rows, you can use `ngClass` or `ngStyle`.
    - Use `index` from `ngFor` to conditionally apply styles based on row position.
    - Example:  
      ```html
      <div *ngFor="let item of items; let i = index" [ngClass]="{'even-row': i % 2 === 0, 'odd-row': i % 2 !== 0}">
          {{ item }}
      </div>
      ```

15. **What is differential loading in Angular? How is it used?**  
   - Differential loading creates two separate JavaScript bundles: one for modern browsers (ES2015+) and one for older browsers (ES5).  
   - Angular CLI handles differential loading automatically during production builds.  
   - It improves performance by serving smaller, optimized bundles to modern browsers.  
   - It includes polyfills only for browsers that require them, reducing the payload for modern ones.  
   - Example: Run `ng build --configuration production` to generate ES2015 and ES5 bundles for modern and legacy browsers.

16. **What is Angular's BehaviorSubject and how does it differ from Subject?**  
   - `BehaviorSubject` retains the last emitted value and emits it to any new subscribers immediately upon subscription.  
   - `Subject` does not hold any value and emits only to existing subscribers when `next()` is called.  
   - `BehaviorSubject` is suitable for state management, while `Subject` is better for events that don’t require state retention.  
   - `BehaviorSubject` requires an initial value when created, whereas `Subject` does not.  
   - Example:  
     ```typescript
     const subject = new Subject<number>();
     const behaviorSubject = new BehaviorSubject<number>(0);

     subject.next(1); // no subscribers, no output
     behaviorSubject.subscribe(console.log); // outputs: 0 (initial value)
     behaviorSubject.next(2); // outputs: 2
     ```

17. **How would you sum all the elements in an array without using a built-in function?**  
   - Use a `for` loop to iterate through the array and calculate the sum manually.  
   - Initialize a variable to store the sum, starting from zero.  
   - Loop through each element of the array and add it to the sum variable.  
   - This approach is useful for custom logic or when using environments without built-in methods.  
   - Example:  
     ```typescript
     const array = [1, 2, 3, 4];
     let sum = 0;
     for (let i = 0; i < array.length; i++) {
         sum += array[i];
     }
     console.log(sum); // Outputs: 10
     ```

18. **What are the key features of Angular Material and Bootstrap?**  
   - **Angular Material** provides pre-built UI components adhering to Material Design specifications. It focuses on Angular-specific needs like dynamic data binding and animations.  
   - **Bootstrap** offers responsive design utilities, grid systems, and general-purpose CSS/JS components. It is framework-agnostic.  
   - Angular Material integrates seamlessly with Angular’s reactive forms and animations, while Bootstrap supports a wide variety of frameworks.  
   - Angular Material is highly customizable with theming support; Bootstrap relies on CSS/SASS for customization.  
   - Example: Use Angular Material’s `MatButtonModule` or Bootstrap’s `btn` class for buttons.  

19. **Can you explain how routing works in Angular, particularly with the routerOutlet component?**  
   - Angular’s routing system uses `Routes` to map URLs to components.  
   - The `RouterOutlet` directive acts as a placeholder for dynamically loaded components based on the route.  
   - The `RouterModule.forRoot(routes)` configures the routes for the application.  
   - Child routes are defined within feature modules for modular routing.  
   - Example:  
     ```typescript
     const routes: Routes = [
         { path: 'home', component: HomeComponent },
         { path: 'about', component: AboutComponent }
     ];
     @NgModule({ imports: [RouterModule.forRoot(routes)], exports: [RouterModule] })
     export class AppRoutingModule {}
     ```

20. **Do you have any Angular running environment at the local?**  
   - Yes, a local development environment typically includes Node.js, Angular CLI, and IDEs like Visual Studio Code.  
   - The Angular CLI (`ng`) is used for scaffolding, building, and serving Angular applications.  
   - A local environment allows for testing and debugging Angular apps during development.  
   - Example: Run `ng serve` to start the development server locally.  
   - I’ve used this for testing new features and debugging issues in Angular projects.

21. **Have you mentioned your testing experience anywhere in your resume?**  
   - Testing experience is highlighted, including unit tests with Jasmine and Karma, and end-to-end testing with Protractor or Cypress.  
   - I also mention integration tests and API mocking where applicable.  
   - Testing libraries such as Jest are also included if used.  
   - Example: "Developed unit tests for services and components, achieving 90%+ test coverage using Jasmine and Karma."

22. **Can you see the component setup on the online Angular compiler?**  
   - Yes, tools like [StackBlitz](https://stackblitz.com) allow online Angular development and testing.  
   - These compilers are useful for quickly prototyping or debugging code.  
   - They provide a real-time preview of the app as changes are made.  
   - Example: Created sample projects on StackBlitz to share implementations during team discussions.  

23. **Do you know how to handle input events on "Enter"?**  
   - Listen for the `keydown` or `keyup` event on the input element.  
   - Check for the `Enter` key (`event.key === 'Enter'`).  
   - Execute the desired logic when the condition is met.  
   - Example:  
     ```typescript
     <input (keydown.enter)="onEnter($event)" placeholder="Press Enter" />
     onEnter(event: any) {
         console.log('Enter key pressed!', event.target.value);
     }
     ```

24. **What is an App Initializer in Angular? How would you use it?**  
   - `APP_INITIALIZER` is a multi-provided token used to execute code before the app bootstraps.  
   - It ensures necessary configuration or data is loaded before the app starts.  
   - It returns a factory function that resolves a `Promise`.  
   - Useful for loading environment settings or user data.  
   - Example:  
     ```typescript
     providers: [
         {
             provide: APP_INITIALIZER,
             useFactory: initApp,
             deps: [ConfigService],
             multi: true
         }
     ]
     function initApp(config: ConfigService) {
         return () => config.loadConfig();
     }
     ```

25. **How would you add Bootstrap to an Angular application? What is the difference between adding it via npm versus a CDN?**  
   - Via npm: Install using `npm install bootstrap` and add it in `angular.json` under styles and scripts.  
   - Via CDN: Add the CDN link to `index.html` for styles and scripts.  
   - NPM is preferred for offline development and build integration, while CDN is faster for loading in production.  
   - Example:  
     ```json
     "styles": ["node_modules/bootstrap/dist/css/bootstrap.min.css"],
     "scripts": ["node_modules/bootstrap/dist/js/bootstrap.min.js"]
     ```

26. **Can you explain the role of the package-lock.json file in Angular projects? How does it handle versioning of dependencies?**  
   - The `package-lock.json` file ensures consistent dependency versions across installations.  
   - It records the exact versions of dependencies and sub-dependencies installed.  
   - Helps to avoid version conflicts by locking the dependency tree.  
   - It is automatically updated when dependencies are added or updated.  
   - Example: "I ensured consistent builds across environments by committing the `package-lock.json` file."

27. **What is the difference between dependencies and devDependencies in Angular?**  
   - **Dependencies**: Required for the application to run, such as Angular core libraries (`@angular/core`).  
   - **DevDependencies**: Required only during development or build time, such as testing tools (`jasmine`, `karma`).  
   - DevDependencies are excluded from production builds.  
   - Example from `package.json`:  
     ```json
     "dependencies": { "@angular/core": "^16.0.0" },
     "devDependencies": { "karma": "^6.3.0" }
     ```

28. **How do you upgrade an Angular application from one version to another? Can you walk through the process?**  
   - Update Angular CLI globally and locally using `npm install -g @angular/cli@latest`.  
   - Use `ng update` to check available updates and dependencies.  
   - Update the framework packages and resolve breaking changes as per Angular's update guide.  
   - Test the application thoroughly after upgrading.  
   - Example: Ran `ng update @angular/core @angular/cli` to upgrade from Angular 15 to 16.  

29. **How can you use multiple RouterOutlet in Angular?**  
   - Multiple `RouterOutlet` instances can be used with named outlets.  
   - Define named outlets in the routes configuration.  
   - Activate the outlets programmatically using `router.navigate()` with outlet names.  
   - Example:  
     ```typescript
     const routes: Routes = [
         { path: 'main', component: MainComponent, outlet: 'primary' },
         { path: 'sidebar', component: SidebarComponent, outlet: 'sidebar' }
     ];
     ```

30. **What is the role of HTTP interceptors in Angular? How do you ensure that a particular interceptor runs first in Angular when multiple interceptors are used?**  
   - HTTP interceptors modify outgoing requests or incoming responses in the HTTP pipeline.  
   - They are implemented using the `HttpInterceptor` interface.  
   -

    The order of execution is determined by the order of their registration in the `providers` array.  
   - Example: Add an authorization header to all requests.  
     ```typescript
     intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
         const cloned = req.clone({ headers: req.headers.set('Authorization', 'Bearer token') });
         return next.handle(cloned);
     }
     ```  

    31. **How do you handle passing children routes in a module-less Angular application?**  
   - In a module-less Angular app, use standalone components with the `standalone: true` property.  
   - Define child routes within the `children` array of the parent route.  
   - Configure the `RouterModule` using `RouterModule.forRoot(routes)` or `forChild(routes)` for lazy-loaded modules.  
   - Ensure components are imported directly in routes without relying on feature modules.  
   - Example:  
     ```typescript
     const routes: Routes = [
         {
             path: 'parent',
             component: ParentComponent,
             children: [
                 { path: 'child', component: ChildComponent }
             ]
         }
     ];
     ```

32. **Can you explain the concept of a "Differ" in Angular and where it is used?**  
   - A differ detects changes in an iterable or key-value collection.  
   - Angular uses differs internally for change detection in structural directives like `ngFor`.  
   - KeyValueDiffers and IterableDiffers detect changes in objects and arrays, respectively.  
   - Custom differs can be created for complex data structures.  
   - Example: `ngFor` updates the DOM only for changed items using IterableDiffers.

33. **What is your experience with Angular, and which versions have you worked with?**  
   - Extensive experience with Angular, starting from Angular 2 to the latest versions like Angular 16/17.  
   - Worked on projects involving reactive forms, material design, and state management using RxJS or NgRx.  
   - Experience includes upgrading Angular apps and implementing modular architecture.  
   - Hands-on with new Angular features like standalone components and Angular Signals.  
   - Example: Migrated an enterprise app from Angular 9 to Angular 16, introducing standalone components.

34. **What is a Cross-Origin Resource Sharing (CORS) error and how do you handle it in Angular?**  
   - A CORS error occurs when a browser blocks requests to a server on a different origin due to security policies.  
   - It is resolved by enabling CORS on the server through headers like `Access-Control-Allow-Origin`.  
   - In development, proxy configurations in Angular can be used to avoid CORS issues.  
   - Example: Configure a proxy in `proxy.conf.json` to redirect API calls during local development.  
   - "I encountered and resolved CORS issues while integrating third-party APIs in Angular projects."

35. **Can you explain Angular directives and the different types (structural, attribute, and component directives)?**  
   - Structural directives (e.g., `*ngIf`, `*ngFor`) alter the DOM structure by adding or removing elements.  
   - Attribute directives (e.g., `ngClass`, `ngStyle`) modify the appearance or behavior of existing elements.  
   - Component directives define reusable UI elements with templates, styles, and logic.  
   - Directives are declared in `declarations` for module-based components or used directly in standalone components.  
   - Example: Created a custom attribute directive to highlight invalid form fields.

36. **What is the difference between a pure pipe and an impure pipe in Angular?**  
   - A pure pipe processes only when its input changes by reference (default behavior).  
   - An impure pipe processes on every change detection cycle, even for same-reference inputs.  
   - Impure pipes are less performant and should be used sparingly.  
   - Mark a pipe as impure using `pure: false` in its metadata.  
   - Example:  
     ```typescript
     @Pipe({ name: 'impurePipe', pure: false })
     export class ImpurePipe implements PipeTransform {
         transform(value: any): any {
             return value.filter(item => item.active);
         }
     }
     ```

37. **What is Track By in Angular and how does it work?**  
   - `trackBy` is used in `ngFor` to uniquely identify items in a list, improving rendering performance.  
   - It prevents Angular from recreating DOM elements unnecessarily during change detection.  
   - Define a `trackBy` function that returns a unique identifier for each item.  
   - Example:  
     ```typescript
     <div *ngFor="let item of items; trackBy: trackById">
         {{ item.name }}
     </div>
     trackById(index: number, item: any): number {
         return item.id;
     }
     ```

38. **How would you handle a large dataset in the DOM?**  
   - Use pagination to load and display smaller chunks of data.  
   - Implement virtual scrolling to render only the visible portion of the dataset.  
   - Optimize change detection using `OnPush` strategy to reduce performance overhead.  
   - Example: Used Angular CDK's `VirtualScrollViewport` for efficient rendering of large datasets.

39. **What is server-side rendering (SSR) in Angular, and how do you implement it?**  
   - SSR renders Angular applications on the server before sending them to the client.  
   - It improves performance and SEO by pre-rendering content.  
   - Implement SSR using Angular Universal.  
   - Example: Run `ng add @nguniversal/express-engine` to set up SSR in an Angular app.  
   - "I implemented SSR for an e-commerce platform to optimize page load times and improve SEO."

40. **What are the best practices to optimize performance in Angular?**  
   - Use lazy loading for feature modules to reduce the initial bundle size.  
   - Employ `OnPush` change detection to minimize unnecessary DOM updates.  
   - Optimize template binding by avoiding expensive computations in HTML.  
   - Enable Ahead-of-Time (AOT) compilation to precompile templates during the build process.  
   - Example: Applied these practices to enhance the performance of a dashboard application with dynamic widgets.  

41. **How would you share data between sibling components in Angular?**  
   - Use a shared service to manage state and facilitate communication between sibling components.  
   - Implement `BehaviorSubject` or `Subject` in the shared service to notify subscribers about data changes.  
   - Inject the shared service into sibling components to access or modify the shared state.  
   - Optionally, use `@Input()` and `@Output()` for intermediate parent-child communication.  
   - Example: Used a shared service with `BehaviorSubject` to sync search filters between a list and a chart component.  

42. **What are Progressive Web Apps (PWA)?**  
   - PWAs are web applications that offer an app-like experience on mobile and desktop devices.  
   - They are installable, work offline, and provide fast performance using Service Workers.  
   - PWAs leverage browser caching to function in low or no network environments.  
   - Add Angular PWA support using `ng add @angular/pwa`.  
   - Example: Built a PWA for an e-commerce site to enable offline browsing of product catalogs.  

43. **How would you create a multi-step form in Angular?**  
   - Use Angular Reactive Forms to manage the form state and validation for each step.  
   - Divide the form into multiple components or sections, one for each step.  
   - Manage navigation and data sharing between steps using a shared service or parent component.  
   - Add form progress tracking and a summary view at the end of the steps.  
   - Example: Built a multi-step registration form for a SaaS application with real-time validation.  

44. **Which form type is better for large forms in Angular?**  
   - Reactive Forms are better for large forms because they provide greater control and flexibility.  
   - They allow dynamic form generation and validation rules assignment.  
   - Form state can be easily tracked and manipulated using the `FormGroup` and `FormControl` APIs.  
   - Example: Used Reactive Forms to dynamically generate a multi-section medical questionnaire.  

45. **How would you get data from a third-party API in Angular?**  
   - Use Angular's `HttpClient` service to make HTTP requests to the API.  
   - Handle asynchronous responses using RxJS operators like `subscribe`, `map`, and `catchError`.  
   - Configure interceptors for shared headers or token-based authentication.  
   - Example: Retrieved real-time weather data using `HttpClient` for a weather forecasting app.  

46. **Have you worked with responsive design? How do you make a design responsive in Angular?**  
   - Use CSS media queries and frameworks like Angular Material or Bootstrap for responsive layouts.  
   - Employ Angular's `FlexLayout` library for grid-based designs.  
   - Utilize viewport-specific directives and conditions in templates for device-specific behavior.  
   - Example: Designed a dashboard that adapts layout and features based on screen size.  

47. **What are the main steps to prevent and troubleshoot performance issues in Angular applications?**  
   - Identify bottlenecks using tools like Chrome DevTools, Angular Profiler, and Lighthouse.  
   - Optimize change detection by switching to `OnPush` strategy where possible.  
   - Minimize the bundle size with lazy loading and AOT compilation.  
   - Reduce redundant HTTP requests by implementing caching in services.  
   - Example: Debugged a sluggish app using Angular Profiler and improved rendering with virtual scrolling.  

48. **Can you explain how to manage state in Angular using services or stores?**  
   - Use Angular services with `BehaviorSubject` or `ReplaySubject` for basic state management.  
   - Implement NgRx or Akita for advanced state management with Redux-style architecture.  
   - Structure the state into actions, reducers, and selectors for clarity and scalability.  
   - Example: Used NgRx to manage user authentication and profile data in a social media app.  

49. **What is the current version of Angular you are working on? What versions have you worked with before?**  
   - Currently working with Angular 16/17, leveraging standalone components and Angular Signals.  
   - Past experience spans Angular 2 to Angular 15, covering both legacy and modern features.  
   - "I have worked extensively on Angular applications in various industries like e-commerce, healthcare, and SaaS."  

50. **What is the difference between authentication and authorization?**  
   - Authentication verifies the identity of a user, ensuring they are who they claim to be.  
   - Authorization determines what resources or actions a user is allowed to access.  
   - Authentication typically involves login credentials, while authorization checks roles/permissions.  
   - Example: Implemented authentication using OAuth2 and role-based authorization for API access control.  

51. **How would you implement route guards in Angular for authorization?**  
   - Use `CanActivate` or `CanActivateChild` guards to restrict access to specific routes.  
   - Implement a guard service that checks user roles or tokens before allowing navigation.  
   - Example:  
     ```typescript
     canActivate(route: ActivatedRouteSnapshot): boolean {
         return this.authService.hasRole(route.data.requiredRole);
     }
     ```  

52. **What is the difference between canActivate and canLoad guards in Angular?**  
   - `CanActivate` prevents unauthorized navigation to a route.  
   - `CanLoad` prevents lazy-loaded modules from being loaded.  
   - Use `CanLoad` for performance optimization, ensuring restricted modules are never downloaded.  
   - Example: Used `CanLoad` for securing admin modules in a multi-role app.  

53. **How does Angular load and run an application in the DOM? Can you explain the process step-by-step?**  
   - Angular bootstraps the root module and creates the root component.  
   - It initializes the component tree, instantiates services, and processes DI tokens.  
   - The app structure is rendered into the DOM using the `AppComponent`.  
   - Example: Built a custom loader to visualize app initialization stages during bootstrapping.  

54. **How do you change the root component in an Angular application (other than app-root)?**  
   - Update the `bootstrap` array in the root module to include the desired component.  
   - Update the `selector` in the index.html to match the new component's selector.  
   - Example: Switched the root component to `MainComponent` for a multi-tenant Angular app.  

55. **What is the difference between ng build and ng serve commands in Angular?**  
   - `ng build` compiles the app into static files for production or development use.  
   - `ng serve` starts a local development server with live reloading for faster testing.  
   - Example: Used `ng build --prod` to deploy a high-performance build of a web app to production.  


56. **How does ng build work internally? What steps does Angular take to build the application?**  
   - Angular compiles the application using the TypeScript compiler and Ahead-of-Time (AOT) or Just-in-Time (JIT) compilation.  
   - It optimizes code by tree-shaking unused code and minifying assets for production builds.  
   - The `angular.json` file governs build configurations like assets, styles, and environments.  
   - Bundles are generated using Webpack, separating runtime, vendor, and application code.  
   - Example: Used `ng build --configuration production` to create an optimized build for deployment.  

57. **How can you improve the performance of an Angular application?**  
   - Implement lazy loading for feature modules and routes to reduce the initial load time.  
   - Use `OnPush` change detection to minimize unnecessary DOM updates.  
   - Optimize assets using compression, minification, and caching strategies.  
   - Reduce HTTP calls by caching frequently requested data in services.  
   - Example: Enhanced an analytics dashboard's performance by integrating Angular CDK's virtual scrolling.  

58. **What is tree shaking and how does it work in Angular?**  
   - Tree shaking is a build optimization technique that removes unused code during bundling.  
   - Angular uses tools like Webpack and Rollup to analyze imports and eliminate dead code.  
   - It ensures smaller bundle sizes and faster application loading.  
   - Example: Observed a 30% reduction in bundle size by removing unused third-party libraries.  

59. **Have you worked with lazy loading in Angular? How does it help in performance optimization?**  
   - Lazy loading defers the loading of feature modules until they are required by the user.  
   - It reduces the initial load time and improves application performance.  
   - Define lazy-loaded routes using the `loadChildren` property in the routing configuration.  
   - Example: Implemented lazy loading for an admin panel to enhance the startup time of an e-commerce platform.  

60. **How do you handle data binding in Angular (e.g., input/output bindings)?**  
   - Use `@Input()` for passing data from a parent to a child component.  
   - Use `@Output()` with `EventEmitter` for emitting events from a child to a parent component.  
   - Example:  
     ```typescript
     @Input() item: string;
     @Output() onItemSelect = new EventEmitter<string>();
     ```  
     "I used this pattern to synchronize selected items between a list and a parent container."  

61. **What is the difference between @Input() and @Output() decorators in Angular?**  
   - `@Input()` allows passing data from a parent to a child component.  
   - `@Output()` emits events from a child to a parent, enabling interaction.  
   - Example: Created reusable dropdown components with `@Input()` for options and `@Output()` for selection events.  

62. **What are lifecycle hooks in Angular? Can you explain the common ones you use?**  
   - `ngOnInit`: Initialization logic runs after the constructor.  
   - `ngOnChanges`: Runs when input-bound properties change.  
   - `ngAfterViewInit`: Executes after child components and DOM elements are initialized.  
   - Example: Used `ngOnInit` to fetch initial data for dashboard components.  

63. **What is the difference between ngOnChanges and ngOnInit lifecycle hooks?**  
   - `ngOnChanges` runs whenever input properties change; ideal for reacting to data updates.  
   - `ngOnInit` runs once when the component initializes, used for setup logic.  
   - Example: Used `ngOnChanges` to dynamically update charts when data input changes.  

64. **What is change detection in Angular? How does it work?**  
   - Change detection is a mechanism Angular uses to track and update the DOM when component data changes.  
   - It runs a digest cycle to compare component properties and template bindings.  
   - Example: Optimized performance using `ChangeDetectionStrategy.OnPush` for static content-heavy pages.  

65. **What is the purpose of OnPush change detection strategy in Angular? When should it be used?**  
   - `OnPush` change detection updates the view only when input bindings change by reference.  
   - It enhances performance by skipping redundant checks.  
   - Example: Applied `OnPush` strategy to a large data table to reduce unnecessary updates.  

66. **What is ngZone in Angular, and how is it used internally by Angular for change detection?**  
   - `ngZone` is a service that helps Angular detect asynchronous operations and trigger change detection.  
   - It wraps browser APIs (e.g., `setTimeout`) to notify Angular when updates are needed.  
   - Example: Used `NgZone.runOutsideAngular()` to handle heavy tasks without triggering unnecessary updates.  

67. **Have you used pipes in Angular? Can you explain how they are used?**  
   - Pipes transform displayed data in templates (e.g., `date`, `currency`).  
   - Create custom pipes by implementing the `PipeTransform` interface.  
   - Example: Developed a `capitalize` pipe to format user input in forms dynamically.  

68. **How would you implement authorization in an Angular app using route guards?**  
   - Create a guard implementing `CanActivate` to verify user roles or tokens.  
   - Use the guard in the route configuration to secure specific routes.  
   - Example: Restricted admin routes in a project using a role-based guard.  

69. **How would you bind data to a component from a service in Angular?**  
   - Inject the service into the component and use its methods or observables to fetch data.  
   - Bind the data to the component's template using interpolation or directives like `ngIf` and `ngFor`.  
   - Example:  
     ```typescript
     this.dataService.getItems().subscribe(items => this.items = items);
     ```  
     "I used this approach for dynamic rendering of a product list in a shopping app."  

70. **How can you pass data between components in Angular?**  
   - Use `@Input`/`@Output` decorators for parent-child communication.  
   - Use a shared service with `BehaviorSubject` for sibling components.  
   - Example: Used a shared service to synchronize user preferences across different sections of a settings page.  

71. **What is the role of a service in Angular?**  
   - Services in Angular centralize business logic and data sharing across components.  
   - They provide reusable methods, which help maintain separation of concerns.  
   - Angular’s Dependency Injection (DI) system allows services to be easily shared.  
   - They can be singleton by default when provided in the root module (`providedIn: 'root'`).  
   - Example: Used a logging service in an Angular project to record user interactions across components.  

72. **Which version of Angular are you currently working on?**  
   - Currently working with Angular 16/17, utilizing new features like standalone components and Signals.  
   - Have worked on Angular versions from 2 to 15, covering major updates like Ivy and Angular Material.  
   - Angular 16 introduced improvements like enhanced SSR, Signals, and developer ergonomics.  
   - The experience includes migration projects from AngularJS to Angular and major version upgrades.  
   - Example: Leveraged Angular 16’s Signals for state management in a real-time chat application.  

73. **Can you explain any new features introduced in Angular 16?**  
   - Signals: A new reactive primitive to track and update application state.  
   - Standalone APIs are now the default for building module-less Angular apps.  
   - Improved Hydration for server-side rendering (SSR) to boost client performance.  
   - Dependency Injection enhancements, including zone-less execution optimizations.  
   - Example: Replaced `BehaviorSubject` with Signals for state management in an admin dashboard.  

74. **What happens if you don’t import a component into the module where you want to use it?**  
   - Angular will throw a template compilation error stating the component is not recognized.  
   - Components must be declared in an `NgModule` or imported if declared elsewhere.  
   - For standalone components, they need to be imported directly into the consuming module/component.  
   - Example: Encountered this issue in a project and resolved it by adding the missing component to the declarations array.  

75. **What frameworks other than Angular have you worked with?**  
   - Proficient in frameworks like React (functional and class-based components).  
   - Experience with Vue.js for lightweight front-end development.  
   - Familiar with backend frameworks like Express.js and Spring Boot for API integration.  
   - Used these frameworks in multi-stack projects to build dynamic, interactive applications.  
   - Example: Combined Angular and Spring Boot for an enterprise-level CRM system.  

76. **In an e-commerce project, how did you handle large datasets?**  
   - Implemented server-side pagination to fetch only required data.  
   - Used Angular CDK’s virtual scrolling to render visible items only.  
   - Leveraged caching for frequently accessed datasets using services.  
   - Integrated lazy loading to defer loading non-essential modules.  
   - Example: Optimized product listing for a retail site with over 10,000 items using virtual scrolling.  

77. **What is Infinite Scroll in Angular?**  
   - Infinite scroll loads additional data as the user scrolls, creating a seamless UX.  
   - Detect the scroll position using Angular event listeners or CDK’s `ScrollViewport`.  
   - Fetch data dynamically using services and append it to the current dataset.  
   - Handle loading states and errors gracefully for a smooth experience.  
   - Example: Built an infinite scrolling feed for a social media app using RxJS observables.  

78. **How do you optimize Angular application performance (e.g., lazy loading, bundle size)?**  
   - Apply lazy loading to feature modules and routes.  
   - Use AOT compilation for faster and smaller builds.  
   - Optimize template bindings using `OnPush` strategy and immutability patterns.  
   - Example: Reduced initial load time of a finance dashboard by splitting heavy charts into lazy-loaded modules.  

79. **How can you check which models/components are taking time to load or increasing the bundle size?**  
   - Use Angular CLI’s `ng build --stats-json` to generate a bundle statistics file.  
   - Analyze the stats using tools like Webpack Bundle Analyzer or Source Map Explorer.  
   - Debug performance with Chrome DevTools or Angular Profiler.  
   - Example: Identified and replaced a large third-party library with a lightweight alternative to optimize a client app.  

80. **What is the purpose of the angular.json file?**  
   - `angular.json` is the workspace configuration file for Angular CLI projects.  
   - It manages build options, global assets, styles, and environment-specific settings.  
   - Controls optimization, budgets, and output paths for builds.  
   - Example: Updated `angular.json` to include new global CSS and configure production builds.  

81. **How do you run unit tests in Angular?**  
   - Use the Angular CLI command `ng test` to execute unit tests via Karma.  
   - Write tests using Jasmine, and Angular’s TestBed for component/service testing.  
   - Mock dependencies with libraries like `jasmine.createSpyObj` or Angular's `HttpTestingController`.  
   - Example: Developed unit tests for a login form, achieving 95% code coverage using Angular CLI.  

82. **Have you used tools like SonarQube for code quality checks?**  
   - SonarQube ensures code quality by detecting bugs, vulnerabilities, and smells.  
   - Integrated SonarQube with CI/CD pipelines for automated checks.  
   - Followed code quality improvements suggested by SonarQube during PR reviews.  
   - Example: Used SonarQube in a healthcare project to meet strict security standards and ensure quality.  

83. **What is the difference between ngOnInit and constructor in Angular components?**  
   - Constructor initializes class members but should not contain Angular logic.  
   - `ngOnInit` is invoked after Angular sets up input bindings, ideal for initialization logic.  
   - Example: Used `ngOnInit` for making initial API calls and avoided calling APIs in the constructor.  

84. **What is the lifecycle of a component in Angular, and why is the constructor called before ngOnInit?**  
   - Constructor initializes the component's instance.  
   - `ngOnInit` executes after constructor and input bindings, ensuring data is ready.  
   - Example: Initialized a user service in the constructor and fetched user data in `ngOnInit`.  

85. **What is a route guard in Angular?**  
   - A route guard determines if a user can access or load a route.  
   - Guards include `CanActivate`, `CanLoad`, `CanActivateChild`, `CanDeactivate`, and `Resolve`.  
   - Example: Used `CanActivate` to restrict dashboard access to authenticated users only.


86. **What is the purpose of directives in Angular? Can you explain Angular directives and the different types (structural, attribute, and component directives)?**  
   - Directives in Angular are instructions that enhance or modify the behavior of DOM elements.  
   - **Structural Directives**: Change the structure of the DOM (e.g., `*ngIf`, `*ngFor`, `*ngSwitch`).  
   - **Attribute Directives**: Change the appearance or behavior of an element (e.g., `[style]`, `[class]`, `ngStyle`, `ngClass`).  
   - **Component Directives**: Special directives with templates, extending the view (essentially Angular components).  
   - Example: Used `*ngFor` for iterating over lists and `ngClass` to apply dynamic styles in a project.  

87. **What is the difference between a component and a directive in Angular?**  
   - A component is a directive with a template, designed to encapsulate UI and logic.  
   - A directive without a template modifies the behavior or appearance of DOM elements.  
   - Components are always used with a selector (e.g., `<app-header>`), whereas directives can apply directly to elements.  
   - Example: Used a custom directive to highlight invalid form fields, enhancing UX across the app.  

88. **What is HostBinding and HostListener in Angular?**  
   - `HostBinding` binds a property of the host element to a directive/component property.  
   - `HostListener` listens to events on the host element and triggers corresponding methods.  
   - These features enable better interaction and customization for directives.  
   - Example:  
     ```typescript
     @HostBinding('class.active') isActive = false;
     @HostListener('click') toggleActive() { this.isActive = !this.isActive; }
     ```  
     "Used `HostBinding` and `HostListener` to implement a toggle button behavior in an interactive dashboard."  

89. **How do you pass data to a directive in Angular?**  
   - Pass data to directives using `@Input` binding.  
   - Bind a value to the directive attribute in the template.  
   - Ensure the directive processes the input dynamically based on the data.  
   - Example:  
     ```typescript
     @Input() appHighlightColor: string;
     @HostBinding('style.color') get color() { return this.appHighlightColor; }
     ```  
     "Used this approach to build a reusable directive for dynamic text highlighting based on user input."  

90. **How do you handle memory leaks in Angular applications?**  
   - Unsubscribe from Observables manually or use `takeUntil` with `Subject` to clean up subscriptions.  
   - Use Angular's `OnDestroy` lifecycle hook to clean up resources like event listeners or timers.  
   - Avoid retaining references to unused components or services.  
   - Example: Prevented memory leaks by unsubscribing from a WebSocket service in a stock-trading app.

