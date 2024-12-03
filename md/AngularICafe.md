**1. What is Routing Guard in Angular?**  
- Routing Guards control navigation to and from routes in an Angular application.  
- Common types include `CanActivate`, `CanDeactivate`, `Resolve`, and `CanLoad`.  
- Guards are implemented using classes that implement a specific guard interface.  
- Example: To protect a route, use `CanActivate`.  
```typescript
@Injectable({ providedIn: 'root' })
export class AuthGuard implements CanActivate {
  canActivate(): boolean {
    return !!localStorage.getItem('token'); // Allow only if token exists
  }
}
const routes: Routes = [{ path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] }];
```

**2. What is a Module, and what does it contain?**  
- A module is a container for components, directives, pipes, and services.  
- Every Angular app has at least one module, the `AppModule`.  
- Modules group related functionalities and can be lazy-loaded for optimization.  
- Example: Import and declare components in `NgModule`.  
```typescript
@NgModule({
  declarations: [AppComponent, DashboardComponent],
  imports: [BrowserModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

**3. What’s the difference between an Angular Component and a Module?**  
- A module organizes the structure of an app, while a component handles the UI and logic.  
- Modules are defined with `@NgModule`, and components are defined with `@Component`.  
- Components belong to a module and require their module to run.  
- Example: A `UserModule` manages user-related components, such as `UserProfileComponent`.

**4. How would you protect a component from being activated through the router?**  
- Use a `CanActivate` guard.  
- Implement logic to check user permissions or authentication.  
- Attach the guard to the desired route.  
- Example:  
```typescript
@Injectable({ providedIn: 'root' })
export class AuthGuard implements CanActivate {
  canActivate(route: ActivatedRouteSnapshot): boolean {
    return route.queryParams['role'] === 'admin';
  }
}
```

**5. What are Observables?**  
- Observables are data streams used for handling asynchronous events.  
- Provided by RxJS, they support operations like mapping, filtering, and merging.  
- Observables are lazy and execute only upon subscription.  
- Example: Fetching data with `HttpClient`.  
```typescript
this.http.get('/api/users').subscribe(data => console.log(data));
```

**6. How would you run unit tests in Angular?**  
- Angular uses Karma as the default test runner.  
- Write test cases using Jasmine framework.  
- Run tests with the `ng test` command.  
- Example: A basic component test.  
```typescript
it('should create the app', () => {
  const fixture = TestBed.createComponent(AppComponent);
  const app = fixture.componentInstance;
  expect(app).toBeTruthy();
});
```

**7. What is the difference between *ngIf vs ngIf [hidden]?**  
- `*ngIf` removes or adds elements to the DOM.  
- `[hidden]` only hides elements via `display: none`.  
- `*ngIf` is better for performance when toggling large sections.  
- Example:  
```html
<div *ngIf="isVisible">Visible</div>
<div [hidden]="!isVisible">Hidden</div>
```

**8. What is Interpolation in Angular?**  
- Interpolation binds data from a component to the template.  
- Uses `{{ expression }}` syntax to display dynamic values.  
- Interpolation can evaluate simple expressions.  
- Example:  
```html
<h1>Hello {{ username }}</h1>
```

**9. You have an HTML response I want to display. How do I do that?**  
- Use `[innerHTML]` to bind HTML safely.  
- Sanitize the response if needed to prevent XSS attacks.  
- Use `DomSanitizer` for trusted content.  
- Example:  
```typescript
this.safeHtml = this.sanitizer.bypassSecurityTrustHtml(responseHtml);
```

**10. What is the difference between @Component and @Directive in Angular?**  
- `@Component` creates UI elements; `@Directive` modifies behavior or appearance.  
- Components must have a template; directives don’t.  
- Use `@Directive` for attribute and structural modifications.  
- Example:  
```typescript
@Directive({
  selector: '[highlight]'
})
export class HighlightDirective {
  constructor(el: ElementRef) {
    el.nativeElement.style.backgroundColor = 'yellow';
  }
}
```

**11. What is an Observer in Angular?**  
- An observer listens to observable streams.  
- It responds to `next`, `error`, or `complete` notifications.  
- Observers must implement `Observer<T>` interface.  
- Example:  
```typescript
const observer = {
  next: (value) => console.log(value),
  error: (err) => console.error(err),
  complete: () => console.log('Complete')
};
observable$.subscribe(observer);
```

**12. What is the difference between Structural and Attribute directives in Angular?**  
- Structural directives change the DOM layout, e.g., `*ngIf`, `*ngFor`.  
- Attribute directives change the appearance/behavior, e.g., `[ngClass]`.  
- Structural directives begin with an asterisk.  
- Example:  
```html
<div *ngIf="isVisible">Visible</div>
<div [ngClass]="{'highlight': isActive}"></div>
```

**13. What is a bootstrapping module in Angular?**  
- The root module bootstraps the Angular app.  
- It declares the entry component for application rendering.  
- Usually defined as `AppModule`.  
- Example:  
```typescript
platformBrowserDynamic().bootstrapModule(AppModule);
```

**14. What is the purpose of the base href tag?**  
- Specifies the base URL for resolving relative paths in the app.  
- Enables Angular’s routing to interpret paths correctly.  
- Located in `index.html` as `<base href="/">`.  
- Example: For a deployment under `/app/`, set `<base href="/app/">`.

**15. What is the equivalent of ngShow and ngHide in Angular?**  
- Use `[hidden]` or `*ngIf` for show/hide functionality.  
- `[hidden]` retains elements in the DOM.  
- `*ngIf` removes or adds elements dynamically.  
- Example:  
```html
<div [hidden]="!isVisible">Hidden</div>
<div *ngIf="isVisible">Visible</div>
```

**16. What is an Observable?**  
- An observable is a stream of asynchronous data that emits multiple values over time.  
- It provides powerful operators like `map`, `filter`, and `merge`.  
- Observables are lazy and require a subscription to begin execution.  
- Example: Using `HttpClient` to fetch data as an observable.  
```typescript
this.http.get('/api/data').subscribe(response => console.log(response));
```

**17. What is the minimum definition of a Component?**  
- A component requires a selector, template or template URL, and metadata.  
- Defined with the `@Component` decorator.  
- At least one root component must exist in an Angular application.  
- Example:  
```typescript
@Component({
  selector: 'app-hello',
  template: '<h1>Hello, World!</h1>'
})
export class HelloComponent {}
```

**18. What are the differences between AngularJS (Angular 1.x) and Angular (Angular 2.x and beyond)?**  
- Angular uses TypeScript, whereas AngularJS uses JavaScript.  
- Angular has a component-based architecture; AngularJS uses controllers and scope.  
- Angular provides better performance with AOT and Ivy Renderer.  
- Example: Angular uses modules (`@NgModule`), whereas AngularJS uses modules with dependency injection.  

**19. What is a Custom Component? Why would you use it?**  
- A custom component is a user-defined, reusable UI building block.  
- It encapsulates template, style, and logic for specific functionality.  
- Used to maintain modularity and code reuse in applications.  
- Example:  
```typescript
@Component({
  selector: 'app-user-card',
  template: '<div>{{ user.name }}</div>'
})
export class UserCardComponent {
  @Input() user: any;
}
```

**20. What is a Service, and when will you use it?**  
- Services handle reusable logic, such as data fetching and business logic.  
- They provide dependency injection for components.  
- Services are shared across components for better maintainability.  
- Example: Creating a user service for API calls.  
```typescript
@Injectable({ providedIn: 'root' })
export class UserService {
  constructor(private http: HttpClient) {}
  getUsers() {
    return this.http.get('/api/users');
  }
}
```

**21. Explain how Custom Elements work internally.**  
- Custom elements are web components defined with Angular components.  
- Angular creates these as native browser elements via `@angular/elements`.  
- They encapsulate functionality, making them reusable in non-Angular projects.  
- Example: Convert a component into a custom element.  
```typescript
const userCardElement = createCustomElement(UserCardComponent, { injector });
customElements.define('user-card', userCardElement);
```

**22. When would you use Lazy Loading in Angular?**  
- Lazy loading loads modules only when required, improving app performance.  
- Used for large apps to reduce initial load time.  
- Implemented using Angular’s router with `loadChildren`.  
- Example:  
```typescript
const routes: Routes = [
  { path: 'admin', loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule) }
];
```

**23. What is a Parameterized Pipe?**  
- A pipe that takes arguments to transform data dynamically.  
- Examples include `date`, `currency`, and `slice` pipes.  
- Custom parameterized pipes can be created.  
- Example:  
```html
<p>{{ price | currency:'USD':true }}</p>
```

**24. What is Bazel in Angular?**  
- Bazel is a build tool for efficient, incremental builds in Angular.  
- It provides fine-grained control over build outputs.  
- Enables faster builds and tests in large-scale projects.  
- Example: Configuring Bazel for Angular CLI.  
```bash
ng new my-app --collection=@angular/bazel
```

**25. How do you categorize data binding types in Angular?**  
- Interpolation: `{{ expression }}` for one-way binding from component to DOM.  
- Property binding: `[property]="value"` for dynamic DOM updates.  
- Event binding: `(event)="handler"` for handling user actions.  
- Two-way binding: `[(ngModel)]` to bind both property and event.  
- Example:  
```html
<input [(ngModel)]="username">
```

**26. What is Multicasting in RxJS?**  
- Multicasting shares a single observable execution among multiple subscribers.  
- Achieved using subjects like `BehaviorSubject` or `ReplaySubject`.  
- Reduces redundant operations and improves efficiency.  
- Example:  
```typescript
const subject = new BehaviorSubject(0);
subject.subscribe(value => console.log('Subscriber A:', value));
subject.subscribe(value => console.log('Subscriber B:', value));
subject.next(1);
```

**27. What are the utility functions provided by RxJS?**  
- Common utilities include `of`, `from`, `merge`, `concat`, `combineLatest`, and `forkJoin`.  
- These functions create observables and manipulate data streams.  
- Widely used for complex asynchronous tasks.  
- Example: Combine multiple streams.  
```typescript
combineLatest([stream1, stream2]).subscribe(([a, b]) => console.log(a, b));
```

**28. Do I always need a Routing Module in Angular?**  
- Routing modules are optional but recommended for modularity in apps with routing.  
- For small apps, routes can be defined in `AppModule`.  
- A separate routing module simplifies route management in large apps.  
- Example:  
```typescript
@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class AdminRoutingModule {}
```

**29. What are the ways to control AOT compilation?**  
- Enable AOT explicitly with `ng build --aot`.  
- Use `angular.json` to set AOT as default.  
- Optimize build pipelines by controlling template and metadata precompilation.  
- Example: Configuring AOT in `angular.json`.  
```json
"build": {
  "options": {
    "aot": true
  }
}
```

**30. What is Router Outlet in Angular?**  
- `RouterOutlet` is a placeholder to load routed components dynamically.  
- It acts as a viewport in a template for routing.  
- Supports named outlets for rendering multiple routes.  
- Example:  
```html
<router-outlet></router-outlet>
```

**31. Explain Lazy Loading in Angular.**  
- Lazy loading is a technique to load modules only when their routes are accessed.  
- It helps reduce the initial load time of the application.  
- Configured using the `loadChildren` property in the route definitions.  
- Example:  
```typescript
const routes: Routes = [
  { path: 'feature', loadChildren: () => import('./feature/feature.module').then(m => m.FeatureModule) }
];
```

**32. How to inject the base href in Angular?**  
- Angular uses the `APP_BASE_HREF` token to configure the base path.  
- You can set it explicitly in the providers array.  
- Alternatively, it can be dynamically determined using `document.baseURI`.  
- Example:  
```typescript
providers: [{ provide: APP_BASE_HREF, useValue: '/my-app/' }]
```

**33. What is Protractor in Angular?**  
- Protractor is an end-to-end testing framework for Angular applications.  
- It automates interaction with web elements for UI testing.  
- Works seamlessly with Angular’s elements like `ng-model` and `ng-repeat`.  
- Example:  
```typescript
it('should display the title', async () => {
  await browser.get('/');
  const title = await element(by.css('h1')).getText();
  expect(title).toBe('My App');
});
```

**34. What is the Activated Route in Angular?**  
- `ActivatedRoute` provides access to the route's parameters, data, and query parameters.  
- It is an injectable service available for the current route.  
- It enables reactive programming with observables for route changes.  
- Example:  
```typescript
constructor(private route: ActivatedRoute) {
  this.route.params.subscribe(params => console.log(params['id']));
}
```

**35. What is the purpose of a Wildcard route?**  
- Wildcard routes handle undefined or fallback paths.  
- They are typically defined as the last route in the configuration.  
- Prevents users from accessing undefined routes.  
- Example:  
```typescript
const routes: Routes = [
  { path: '**', component: PageNotFoundComponent }
];
```

**36. What is Router State in Angular?**  
- Router state refers to the state of the router at a given point in navigation.  
- It includes the activated route tree and snapshot of the route.  
- Provides information like parameters, data, and URLs.  
- Example: Accessing `RouterStateSnapshot`.  
```typescript
constructor(private router: Router) {
  console.log(this.router.routerState.snapshot.url);
}
```

**37. What are Custom Elements in Angular?**  
- Custom elements are Angular components transformed into native web components.  
- They are compatible with any framework or plain HTML.  
- Created using `@angular/elements` package.  
- Example:  
```typescript
const customEl = createCustomElement(MyComponent, { injector });
customElements.define('my-component', customEl);
```

**38. What is the difference between Promise and Observable in Angular?**  
- Promises are eager and resolve once, while observables are lazy and emit multiple values.  
- Observables support operators for transformation and composition.  
- Observables are cancellable, but promises are not.  
- Example: Observables for real-time data.  
```typescript
this.data$.subscribe(value => console.log(value));
```

**39. What happens if you use a `<script>` tag inside the template?**  
- Angular sanitizes and removes `<script>` tags for security reasons.  
- It prevents cross-site scripting (XSS) vulnerabilities.  
- Use `[innerHTML]` with sanitized content for dynamic script embedding.  
- Example: Using `DomSanitizer` for safe HTML.  
```typescript
this.trustedHtml = this.sanitizer.bypassSecurityTrustHtml('<div>Hello</div>');
```

**40. What is Angular Ivy Renderer?**  
- Ivy is Angular's next-generation rendering engine introduced in Angular 9.  
- It optimizes bundle sizes and improves compilation speed.  
- Offers better debugging with human-readable code.  
- Example: Enabling Ivy in `angular.json`.  
```json
"angularCompilerOptions": {
  "enableIvy": true
}
```

**41. What is Subscribing in Angular?**  
- Subscribing starts the execution of an observable.  
- It listens for data emissions (`next`), errors, or completion of the observable.  
- Required for consuming asynchronous streams like HTTP requests.  
- Example:  
```typescript
this.http.get('/api/data').subscribe(data => console.log(data));
```

**42. What are dynamic components?**  
- Dynamic components are created and loaded at runtime.  
- Useful for modular and reusable UI elements.  
- Achieved using `ComponentFactoryResolver` or `ViewContainerRef`.  
- Example:  
```typescript
const factory = this.resolver.resolveComponentFactory(MyComponent);
this.container.createComponent(factory);
```

**43. What is the option to choose between Inline and External template files?**  
- Inline templates are defined directly in the `template` property.  
- External templates are specified with `templateUrl` and loaded as separate files.  
- Inline templates are suitable for small, simple components.  
- Example:  
```typescript
@Component({
  selector: 'app-inline',
  template: '<h1>Hello Inline!</h1>'
})
export class InlineComponent {}
```

**44. Why does Incremental DOM have a low memory footprint?**  
- It directly manipulates the DOM without creating intermediate structures.  
- Only updates changed elements, minimizing overhead.  
- Eliminates the need for virtual DOM reconciliation.  
- Example: Angular Ivy uses Incremental DOM for efficient rendering.

**45. How do you perform Error Handling for HttpClient in Angular?**  
- Use `catchError` operator to handle HTTP errors.  
- Optionally, log errors using a service for monitoring.  
- Show user-friendly error messages in the UI.  
- Example:  
```typescript
this.http.get('/api/data').pipe(
  catchError(err => {
    console.error('Error occurred:', err);
    return of([]); // Return fallback data
  })
).subscribe();
```

**46. How do you perform error handling in Observable in Angular?**  
- Use the `catchError` operator in the observable pipeline to intercept errors.  
- Combine with `retry` or `retryWhen` for automatic retries on failure.  
- Gracefully handle errors by providing fallback values or logging them.  
- Example:  
```typescript
this.data$.pipe(
  catchError(err => {
    console.error('Error:', err);
    return of([]); // Provide fallback data
  })
).subscribe(data => console.log(data));
```

**47. What is Angular Universal?**  
- Angular Universal enables server-side rendering (SSR) for Angular apps.  
- Improves SEO and performance by rendering pages on the server.  
- Uses `@nguniversal/express-engine` for Node.js server integration.  
- Example:  
```bash
ng add @nguniversal/express-engine
npm run build:ssr
npm run serve:ssr
```

**48. What is TestBed in Angular?**  
- `TestBed` is a testing utility that creates an Angular testing module.  
- Configures components, services, and modules for testing.  
- Allows mocking dependencies and simulating real scenarios.  
- Example:  
```typescript
TestBed.configureTestingModule({
  declarations: [MyComponent],
  providers: [MyService]
}).compileComponents();
```

**49. What is Redux, and how does it relate to an Angular app?**  
- Redux is a predictable state management library for JavaScript apps.  
- It centralizes app state in a single store, making debugging easier.  
- Integrated into Angular via libraries like `ngrx/store`.  
- Example:  
```typescript
store.dispatch({ type: '[User] Load', payload: userId });
store.select('user').subscribe(data => console.log(data));
```

**50. What is the use of Codelyzer in Angular?**  
- Codelyzer is a static analysis tool for Angular TypeScript projects.  
- Enforces Angular coding standards and best practices.  
- Works as a TSLint plugin to provide linting rules for Angular.  
- Example:  
```bash
npm install --save-dev codelyzer
ng lint
```

**51. What’s new in Angular 6, and why should we upgrade to it?**  
- Introduced `ng update` for automated dependency updates.  
- Added `RxJS 6` with improved operators and better performance.  
- Included support for Angular Elements to create custom web components.  
- Example: Angular CLI workspace feature for managing multiple projects.  

**52. Can you explain the difference between Promise and Observable in Angular? In what scenario can we use each case?**  
- Promises handle single asynchronous events, while observables handle streams.  
- Observables support operators for chaining and transformation.  
- Use Promises for simple, one-time HTTP requests and Observables for streams like real-time updates.  
- Example:  
```typescript
const observable$ = this.http.get('/api').subscribe(data => console.log(data));
```

**53. What is the difference between declarations, providers, and imports in NgModule?**  
- `Declarations`: Components, directives, and pipes that belong to this module.  
- `Providers`: Services available throughout the app via dependency injection.  
- `Imports`: Other modules whose exported components and services are needed.  
- Example:  
```typescript
@NgModule({
  declarations: [MyComponent],
  imports: [CommonModule],
  providers: [MyService]
})
export class MyModule {}
```

**54. Why should ngOnInit be used if we already have a constructor?**  
- Constructor is for dependency injection and initialization of the object.  
- `ngOnInit` is specifically designed for component initialization logic.  
- Ensures properties are set and bindings are available.  
- Example:  
```typescript
ngOnInit() {
  this.loadData();
}
```

**55. Why would you use a spy in a test?**  
- Spies intercept and mock the behavior of dependencies.  
- Used to test components in isolation without actual service calls.  
- Captures method calls and arguments for verification.  
- Example:  
```typescript
const spy = spyOn(service, 'getData').and.returnValue(of(mockData));
```

**56. What is AOT?**  
- AOT (Ahead-of-Time) compiles Angular HTML and TypeScript code during build time.  
- Reduces runtime errors and improves app performance.  
- Produces optimized and smaller JavaScript bundles.  
- Example: Enable AOT with Angular CLI:  
```bash
ng build --aot
```

**57. Explain the difference between Constructor and ngOnInit.**  
- Constructor is a TypeScript feature for dependency injection and initializing the object.  
- `ngOnInit` is an Angular lifecycle hook for initializing the component.  
- Component bindings and inputs are not guaranteed in the constructor.  
- Example: Use constructor for injection, and `ngOnInit` for setup logic.  

**58. What is the difference between @Component and @Directive in Angular?**  
- `@Component` is used to create UI elements with templates and styles.  
- `@Directive` adds behavior to existing DOM elements.  
- Components are self-contained, while directives work on other elements.  
- Example:  
```typescript
@Directive({
  selector: '[highlight]'
})
export class HighlightDirective {
  @HostListener('mouseenter') onMouseEnter() {
    this.highlight('yellow');
  }
}
```

**59. What is the difference between Promise and Observable in Angular?**  
- Promises are resolved once, Observables emit multiple values over time.  
- Observables provide operators for data transformation.  
- Observables are lazy, while Promises are eager.  
- Example: Real-time chat using Observables vs fetching user data with Promises.

**60. What is Incremental DOM, and how is it different from Virtual DOM?**  
- Incremental DOM updates the DOM directly without creating a virtual representation.  
- Reduces memory overhead and processing time by skipping reconciliation.  
- Angular Ivy uses Incremental DOM for faster and more efficient rendering.  
- Example: Incremental DOM optimizes partial updates rather than full-tree changes.  

**61. Angular 9: What are some new features in Angular 9?**  
- Introduction of Ivy as the default rendering engine.  
- Enhanced debugging with stack traces and better error messages.  
- Improved type-checking for templates in development mode.  
- Example: Smaller bundle sizes with Ivy, enabling faster loads.  

**62. Do I need to bootstrap custom elements?**  
- No, Angular custom elements are bootstrapped automatically by the browser.  
- They are self-contained and registered with `customElements.define()`.  
- Angular handles their lifecycle and change detection internally.  
- Example:  
```typescript
const el = createCustomElement(MyComponent, { injector });
customElements.define('my-element', el);
```

**63. Are there any pros/cons (especially performance-wise) in using local storage to replace cookie functionality?**  
- Pros: Larger storage capacity, faster client-side access, no need for server communication.  
- Cons: Not sent automatically with HTTP requests, less secure than HTTP-only cookies.  
- Suitable for non-sensitive, client-side data storage.  
- Example: Storing user preferences.  
```typescript
localStorage.setItem('theme', 'dark');
```

**64. What are the lifecycle hooks for components and directives in Angular?**  
- `ngOnChanges`: Called when input properties change.  
- `ngOnInit`: Invoked after the component is initialized.  
- `ngOnDestroy`: Triggered before the component is destroyed.  
- Example:  
```typescript
ngOnDestroy() {
  this.subscription.unsubscribe();
}
```

**65. How to detect a route change in Angular?**  
- Use the `Router` service’s `events` observable.  
- Filter for `NavigationStart` or `NavigationEnd` events.  
- Can also use `ActivatedRoute` for specific route parameters.  
- Example:  
```typescript
this.router.events.pipe(
  filter(event => event instanceof NavigationStart)
).subscribe(() => console.log('Route changed'));
```

**66. What are the advantages of AOT compilation?**  
- Eliminates runtime template errors by catching them during build time.  
- Reduces app bundle size with optimized code.  
- Improves application performance by compiling templates ahead of time.  
- Example: Production build with AOT.  
```bash
ng build --prod --aot
```

**67. Explain the purpose of Service Workers in Angular.**  
- Service workers enable Progressive Web App (PWA) features like offline access and caching.  
- Handle background tasks and push notifications.  
- Implemented using the `@angular/service-worker` package.  
- Example:  
```bash
ng add @angular/pwa
```

**68. What is the difference between Incremental DOM and Virtual DOM?**  
- Incremental DOM updates DOM directly and skips intermediate representations.  
- Virtual DOM creates a virtual representation for reconciliation before DOM updates.  
- Incremental DOM is more memory-efficient and faster for large apps.  
- Example: Angular Ivy uses Incremental DOM for rendering.  

**69. Why do we need the compilation process in Angular?**  
- Converts templates into JavaScript for rendering efficiency.  
- Enables dependency injection, directives, and component behaviors.  
- Ensures app is optimized for performance during the build process.  
- Example: JIT compilation for dynamic builds, AOT for production.

**70. What is the need for SystemJS in Angular?**  
- SystemJS is a module loader that dynamically loads JavaScript modules.  
- Used in earlier versions of Angular for module resolution.  
- Replaced by Webpack in modern Angular CLI for better bundling.  
- Example: Angular CLI-generated apps use Webpack by default.

**71. Why should we use Bazel for Angular builds?**  
- Bazel enables incremental builds and efficient dependency management.  
- Allows parallel builds for large-scale applications.  
- Facilitates universal builds across multiple languages.  
- Example: Bazel's support for distributed builds in CI pipelines.

**72. How do you create an application to use Webpack?**  
- Install Webpack and dependencies like loaders and plugins.  
- Configure `webpack.config.js` with entry points and output.  
- Replace Angular CLI commands with Webpack-specific scripts.  
- Example:  
```bash
webpack --config webpack.config.js
```

**73. What is Upgrade in Angular?**  
- Upgrade facilitates running AngularJS (1.x) and Angular (2+) side by side.  
- Helps transition legacy apps incrementally to modern Angular.  
- Achieved using `@angular/upgrade` library.  
- Example: Upgrade an AngularJS service.  
```typescript
upgradeAdapter.upgradeNg1Provider('myService');
```

**74. What is Reactive Programming, and how does it relate to Angular?**  
- Reactive programming focuses on asynchronous data streams.  
- RxJS implements reactive programming for Angular applications.  
- Enables event-driven architectures with operators for data transformation.  
- Example: Using `switchMap` for HTTP calls.  
```typescript
this.search$.pipe(
  switchMap(term => this.http.get(`/search?q=${term}`))
).subscribe(results => console.log(results));
```

**75. Name some security best practices in Angular.**  
- Use Angular’s built-in sanitization for user inputs (`DomSanitizer`).  
- Avoid dynamic templates and `<script>` tags in bindings.  
- Implement route guards and authentication mechanisms.  
- Example: Use `HttpInterceptor` to append secure headers.  
```typescript
intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
  const secureReq = req.clone({ headers: req.headers.set('Authorization', 'Bearer token') });
  return next.handle(secureReq);
}
```

**76. When is a lazy-loaded module loaded?**  
- A lazy-loaded module is loaded when its associated route is accessed.  
- It is not part of the main bundle, reducing the initial load time.  
- Configured using `loadChildren` in the route definition.  
- Example:  
```typescript
const routes: Routes = [
  { path: 'feature', loadChildren: () => import('./feature/feature.module').then(m => m.FeatureModule) }
];
```

**77. Why would you use Renderer methods instead of using native element methods?**  
- Renderer methods provide a platform-independent way to manipulate DOM.  
- Helps maintain compatibility across different environments like SSR.  
- Prevents direct DOM access, ensuring secure interactions.  
- Example:  
```typescript
this.renderer.setStyle(element, 'background-color', 'blue');
```

**78. What is Ivy Renderer in Angular?**  
- Ivy is Angular’s new rendering engine introduced in Angular 9.  
- It compiles components into efficient JavaScript code for faster rendering.  
- Supports incremental DOM for memory-efficient updates.  
- Example: Ivy reduces the size of unused components in tree-shaking.  

**79. What does detectChanges do in Angular Jasmine tests?**  
- `detectChanges` triggers change detection for the component.  
- Ensures updates to bindings and the DOM are reflected during tests.  
- Used with `ComponentFixture` in Angular test setups.  
- Example:  
```typescript
fixture.detectChanges();
expect(component.title).toBe('Test Title');
```

**80. What is the difference between a pure and impure pipe in Angular?**  
- A pure pipe runs only when input values change.  
- An impure pipe runs on every change detection cycle, even for unrelated changes.  
- Use pure pipes for performance-critical scenarios.  
- Example:  
```typescript
@Pipe({ name: 'filter', pure: false })
export class FilterPipe {
  transform(items: any[], searchText: string): any[] { /* filtering logic */ }
}
```

**81. Why would you use lazy loading for modules in an Angular app?**  
- Reduces the initial load time by deferring module loading.  
- Improves performance for apps with many features.  
- Helps organize and maintain large codebases.  
- Example: Lazy load a module with route configuration as follows:  
```typescript
{ path: 'admin', loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule) }
```

**82. What are the mapping rules between Angular component and custom element?**  
- Component selector becomes the custom element tag name.  
- Inputs and outputs map to properties and events of the custom element.  
- Styles and encapsulation are retained within the shadow DOM.  
- Example:  
```typescript
@Component({ selector: 'app-my-element', template: `<p>Hello!</p>` })
export class MyElement {}
customElements.define('app-my-element', createCustomElement(MyElement, { injector }));
```

**83. Name and explain some Angular Module Loading examples.**  
- **Eager Loading**: Modules are loaded at the app’s startup.  
- **Lazy Loading**: Modules are loaded when their route is accessed.  
- **Preloading**: Modules are loaded in the background after the app initializes.  
- Example: Configure preloading with `PreloadAllModules`:  
```typescript
RouterModule.forRoot(routes, { preloadingStrategy: PreloadAllModules })
```

**84. What is Zone in Angular?**  
- Zone.js is a library for intercepting and keeping track of asynchronous operations.  
- It ensures Angular detects changes triggered by async tasks.  
- Facilitates seamless DOM updates in response to events.  
- Example: Zone handles events like setTimeout or HTTP requests automatically.  

**85. What would be a good use for NgZone service?**  
- Use `NgZone` to run code outside Angular’s zone to avoid triggering change detection.  
- Re-enter the zone for tasks requiring UI updates.  
- Helps optimize performance in high-frequency async tasks.  
- Example:  
```typescript
this.ngZone.runOutsideAngular(() => {
  setTimeout(() => this.ngZone.run(() => this.updateUI()), 1000);
});
```

**86. How would you insert an embedded view from a prepared TemplateRef?**  
- Use `ViewContainerRef` to create and insert a view.  
- Pass the `TemplateRef` to `createEmbeddedView` of `ViewContainerRef`.  
- Useful for dynamic templates and reusable UI blocks.  
- Example:  
```typescript
this.viewContainerRef.createEmbeddedView(this.templateRef);
```

**87. What does the Just-in-Time (JIT) compiler do?**  
- JIT compiles Angular templates and code at runtime in the browser.  
- Useful for development mode with faster rebuild times.  
- Does not require precompiled templates, unlike AOT.  
- Example: Angular CLI uses JIT by default for development:  
```bash
ng serve
```

**88. What are observable creation functions in RxJS?**  
- Functions like `of`, `from`, `interval`, and `timer` create observables.  
- Enable the creation of different types of streams for various scenarios.  
- Example:  
```typescript
const observable$ = of(1, 2, 3);
observable$.subscribe(val => console.log(val));
```

**89. What is the Locality principle for Ivy?**  
- Locality means each component is compiled independently.  
- Simplifies debugging and enables better tree-shaking.  
- Reduces the coupling between components and modules.  
- Example: Ivy doesn’t need module context for compiling components.  

**90. How would you compare View Engine vs Ivy in Angular?**  
- Ivy has smaller bundle sizes due to tree-shaking; View Engine doesn’t.  
- Ivy uses incremental DOM for faster rendering, while View Engine relies on templates.  
- Ivy supports locality for independent component compilation.  
- Example: Upgrading to Ivy reduces bundle sizes and improves debugging.  

**91. When to use query parameters vs matrix parameters in URLs?**  
- **Query Parameters**: Used to pass data globally, typically for search, filters, or pagination.  
- **Matrix Parameters**: Used for passing parameters specific to a route segment.  
- Query parameters are part of the URL query string (`?param=value`), while matrix parameters use a semicolon (`;param=value`).  
- Example:  
```typescript
// Query parameters
this.router.navigate(['/search'], { queryParams: { q: 'angular' } });
// Matrix parameters
this.router.navigate(['/product', { id: 1, color: 'red' }]);
```

**92. Angular 8: What are some changes in the Location module?**  
- Support for multiple `baseHref` values during runtime.  
- Added support for `Location.getState()` to retrieve history states.  
- Improved handling of hash-based navigation.  
- Example: Retrieve the current state:  
```typescript
const state = this.location.getState();
console.log(state);
```

**93. Angular 9: Explain improvements in Tree-Shaking.**  
- Ivy eliminates unused code more effectively with enhanced tree-shaking.  
- Components and directives are compiled independently, enabling better optimizations.  
- Reduces bundle size by removing unused features and modules.  
- Example: Unused Angular directives no longer inflate the bundle size.  

**94. How does Ivy affect the (Re)build time?**  
- Ivy improves incremental rebuild times due to its locality principle.  
- Uses precompiled code, reducing the need for recompiling unchanged modules.  
- Smaller bundle sizes lead to faster development and testing cycles.  
- Example: Faster component-only rebuilds during development.  

**95. Just-in-Time (JIT) vs Ahead-of-Time (AOT) compilation: Explain the difference.**  
- **JIT**: Compilation happens in the browser during runtime; faster builds but slower runtime.  
- **AOT**: Compilation occurs at build time, resulting in faster runtime and optimized bundles.  
- AOT detects errors at build time, reducing runtime crashes.  
- Example:  
```bash
# JIT
ng serve
# AOT
ng build --prod --aot
```

**96. Do you know how you can run AngularJS and Angular side by side?**  
- Use `@angular/upgrade` for hybrid apps to bridge AngularJS and Angular.  
- Upgrade AngularJS components and services incrementally.  
- Bootstrap the app using `UpgradeModule`.  
- Example:  
```typescript
import { UpgradeModule } from '@angular/upgrade/static';
platformBrowserDynamic().bootstrapModule(AppModule).then(ref => ref.injector.get(UpgradeModule).bootstrap(document.body, ['myApp']));
```

**97. Why does Angular use URL segments?**  
- URL segments allow Angular to parse and handle routes hierarchically.  
- Provides better control over child routes and their parameters.  
- Facilitates matrix parameters for route-specific data.  
- Example: `/product;id=123/details;tab=reviews` uses segments for clarity.  

**98. What is the difference between BehaviorSubject vs Observable in Angular?**  
- **Observable**: Emits values only to subscribers when they subscribe.  
- **BehaviorSubject**: Emits the last emitted value to new subscribers immediately.  
- BehaviorSubject requires an initial value; Observable does not.  
- Example:  
```typescript
const behaviorSubject = new BehaviorSubject('Initial Value');
behaviorSubject.subscribe(value => console.log(value)); // Outputs: 'Initial Value'
```

**99. Name some differences between SystemJS vs Webpack.**  
- **SystemJS**: A dynamic module loader; less optimized for bundling.  
- **Webpack**: A static bundler, handles multiple assets and optimizations.  
- Webpack supports advanced features like lazy loading and tree-shaking.  
- Example: Angular CLI uses Webpack under the hood for builds.  

**100. How would you extract Webpack config from an Angular CLI project?**  
- Angular CLI abstracts Webpack configuration by default.  
- Use `ng eject` in earlier versions (deprecated after Angular 6).  
- Alternative: Use custom builders to override Webpack configuration.  
- Example: Modify configurations using `angular-builders/custom-webpack`.  

**101. Why is Incremental DOM Tree-Shakable?**  
- Incremental DOM directly manipulates the DOM, avoiding intermediate representations.  
- Compiles each component into independent, self-contained code.  
- Unused components are automatically excluded during tree-shaking.  
- Example: Ivy leverages Incremental DOM for tree-shakable builds.  

**102. Why did the Google team go with Incremental DOM instead of Virtual DOM?**  
- Incremental DOM is more memory-efficient for large apps.  
- Updates only the necessary DOM elements, reducing reconciliation overhead.  
- It simplifies Angular’s rendering pipeline with fewer abstractions.  
- Example: Faster rendering for data-heavy apps using Angular Ivy.  

**103. Could you provide some particular examples of using Zone in Angular?**  
- Tracking asynchronous operations like `setTimeout` or `HTTP` requests.  
- Ensuring UI updates automatically in response to async tasks.  
- Useful in debugging with zone-related error stack traces.  
- Example: Zone handles automatic change detection for promises.  

**104. What are Pipes in Angular? Give me an example.**  
- Pipes transform data for presentation in templates.  
- Angular provides built-in pipes like `uppercase`, `date`, and `currency`.  
- Custom pipes can handle domain-specific transformations.  
- Example:  
```typescript
@Pipe({ name: 'square' })
export class SquarePipe {
  transform(value: number): number {
    return value * value;
  }
}
// Usage: {{ 5 | square }} outputs 25
```

**105. What does this line do in Angular?**  
```typescript
this.changeDetectorRef.detectChanges();
```  
- Manually triggers change detection for the component.  
- Useful in scenarios where Angular’s automatic change detection doesn’t suffice.  
- Ensures updates to the DOM after async operations.  
- Example: Force update a component after external state changes.  

**106. How can I select an element in a component template?**  
- Use Angular’s `@ViewChild` or `@ViewChildren` decorators.  
- `ElementRef` provides direct access to the DOM element.  
- Prefer `Renderer2` for DOM manipulations to maintain compatibility.  
- Example:  
```typescript
@ViewChild('myElement') myElement: ElementRef;
ngAfterViewInit() {
  this.renderer.setStyle(this.myElement.nativeElement, 'color', 'red');
}
```

**107. How would you control the size of an element on the resize of the window in a component?**  
- Use Angular’s `HostListener` to listen to window resize events.  
- Adjust the element size dynamically in the handler.  
- Example:  
```typescript
@HostListener('window:resize', ['$event'])
onResize(event: any) {
  this.width = event.target.innerWidth;
}
```  

**108. How to bundle an Angular app for production?**  
- Use `ng build --prod` for an optimized production build.  
- Minifies, compresses, and bundles the code.  
- Enables AOT and tree-shaking by default.  
- Example:  
```bash
ng build --prod --aot
```

**109. How to set headers for every request in Angular?**  
- Use `HttpInterceptor` to intercept outgoing requests.  
- Add headers using `HttpRequest.clone()` method.  
- Example:  
```typescript
intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
  const cloned = req.clone({ headers: req.headers.set('Authorization', 'Bearer token') });
  return next.handle(cloned);
}
```

**110. Could I use jQuery with Angular?**  
- Yes, but it’s not recommended due to potential conflicts with Angular’s DOM handling.  
- Import jQuery and use it within components as needed.  
- Example:  
```typescript
import * as $ from 'jquery';
ngAfterViewInit() {
  $('#myDiv').fadeIn();
}
```