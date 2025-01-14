
### 1. **What is Zone in Angular, and how do you use NgZone for specific tasks?**  
- **Zone.js**: A library used by Angular to track and manage asynchronous operations, ensuring UI updates when required.  
- **NgZone**: Angular's service to run code inside or outside the Angular zone for better control of change detection.  
- **Use Case**: Improves performance by skipping change detection for non-Angular processes.  
- **How to Use**: Use `runOutsideAngular` to bypass change detection, then re-enter with `run` when needed.  
- **Example**:  
  ```typescript
  this.ngZone.runOutsideAngular(() => {
    setTimeout(() => {
      this.ngZone.run(() => console.log('Change detection triggered'));
    }, 1000);
  });
  ```  

---

### 2. **What is Incremental DOM, and how does it differ from Virtual DOM?**  
- **Incremental DOM**: Updates only the DOM nodes that change, instead of creating a virtual copy of the DOM tree.  
- **Virtual DOM**: Creates an in-memory virtual representation of the DOM and compares it with the actual DOM to identify updates.  
- **Differences**:  
  - Incremental DOM is memory efficient and faster for small updates.  
  - Virtual DOM requires extra memory to store the virtual tree.  
- **Why Google Uses Incremental DOM**: It reduces memory usage, which is critical for large-scale apps like Gmail.  
- **Example**: Incremental DOM directly patches the DOM without a diffing process.  

---

### 3. **Changes in Angular 17 Directive Syntax (`ngFor` and `ngIf`)**  
@if:

Concise Conditionals: Replaces traditional *ngIf with a more readable and concise syntax for conditional rendering.

Example:

HTML

<div>
  @if (isLoggedIn) {
    <p>Welcome, user!</p>
  } @else if (isLoading) {
    <p>Loading...</p>
  } @else {
    <p>Please log in.</p>
  }
</div>
@switch:

Simplified Switch Cases: Provides a cleaner way to handle multiple conditions within your templates.

Example:

HTML

<div>
  @switch (selectedOption) {
    @case('option1'):
      <p>Option 1 content</p>
    @case('option2'):
      <p>Option 2 content</p>
    @default:
      <p>Default content</p>
  }
</div>
@for:

Simplified Loops: Offers a more concise and readable syntax for iterating over arrays or collections.

Example:

HTML

<ul>
  @for (let item of items) {
    <li>{{ item.name }}</li>
  }
</ul>
@pipe:

Inline Pipe Transformations: Allows you to apply pipes directly within the template expression.

Example:

HTML

<p>Total: @pipe(currency) {{ total }}</p>
@bind:

Two-Way Binding: Provides a simplified syntax for two-way data binding.

Example:

HTML

<input type="text" @bind(value)="username" /> 
Important Note:

These template expressions are part of ongoing development and their availability may vary depending on the specific Angular version you are using.
Refer to the official Angular documentation for the most up-to-date information and usage guidelines.

---

### 4. **Changes in Angular 16 and 17 for Modules and Component Creation**  
- **Standalone Components**: Components can now be created without modules, making Angular simpler and more modular.  
- **Tree-shakable Providers**: Services are optimized for better performance by removing unused code.  
- **No Need for Modules**: Use `standalone: true` in the component metadata.  
- **Example**:  
  ```typescript
  @Component({
    standalone: true,
    selector: 'app-example',
    template: '<p>Standalone Component</p>',
  })
  export class ExampleComponent {}
  ```  
- **Backward Compatibility**: Traditional module-based architecture is still supported.  

---

### 5. **How to Safely Display HTML Responses**  
- **Security by Angular**: Angular sanitizes the HTML by default to prevent XSS attacks.  
- **Using `DomSanitizer`**: You can mark specific HTML as safe using the `bypassSecurityTrustHtml` method.  
- **Avoid Direct HTML Binding**: Avoid directly using `[innerHTML]` for user-provided or dynamic HTML content.  
- **What Happens with `<script>` Tags**: Angular removes `<script>` tags from HTML to block script execution.  
- **Example**:  
  ```typescript
  constructor(private sanitizer: DomSanitizer) {
    this.safeHtml = this.sanitizer.bypassSecurityTrustHtml('<b>Safe Content</b>');
  }
  ```  

---

### 6. **What are Smart Components vs. Dumb Components?**  
- **Smart Components**:  
  - Handle business logic and interact with services.  
  - Manage the state of the application.  
  - Example:  
    ```typescript
    @Component({
      selector: 'app-smart',
      template: `<app-dumb [data]="items"></app-dumb>`,
    })
    export class SmartComponent {
      items = ['Item1', 'Item2'];
    }
    ```  
- **Dumb Components**:  
  - Focus only on UI and presentation.  
  - Use `@Input` for data and `@Output` for event communication.  
  - Example:  
    ```typescript
    @Component({
      selector: 'app-dumb',
      template: `<div *ngFor="let item of data">{{ item }}</div>`,
    })
    export class DumbComponent {
      @Input() data: string[] = [];
    }
    ```  
- **Communication**: Smart components pass data to dumb components via inputs.  

---

### 7. **How to Prevent Memory Leaks in Angular?**  
- **Use `AsyncPipe`**: Automatically handles subscriptions and unsubscriptions.  
  - Example:  
    ```html
    <div *ngIf="(data$ | async) as data">{{ data }}</div>
    ```  
- **Unsubscribe Manually**: For observable subscriptions, use `ngOnDestroy`.  
  - Example:  
    ```typescript
    ngOnDestroy() {
      this.subscription.unsubscribe();
    }
    ```  
- **Use `takeUntil` with a `Subject`**:  
  - Example:  
    ```typescript
    private destroy$ = new Subject<void>();
    ngOnDestroy() {
      this.destroy$.next();
      this.destroy$.complete();
    }
    ```  
- **Detach Event Listeners**: Remove listeners in `ngOnDestroy`.  

---

### 8. **How to Structure an Angular Project for Scalability?**  
- **Use Feature Modules**: Split features into their own modules for better organization.  
- **Shared Module**: Place reusable components, directives, and pipes here.  
- **Lazy Loading**: Load modules only when needed to improve performance.  
- **Example Structure**:  
  ```
  src/
  ├── app/
  │   ├── core/ (Singleton services, app-wide features)
  │   ├── shared/ (Reusable components, directives, pipes)
  │   ├── feature-module/ (Specific feature logic)
  ```  
- **Follow Naming Conventions**: Use consistent naming for files and folders.

---

### 9. **How to Manage Shared Components in an Angular Project?**  
- **Create a Shared Module**: Declare and export all shared components, pipes, and directives.  
  - Example:  
    ```typescript
    @NgModule({
      declarations: [SharedComponent],
      exports: [SharedComponent],
    })
    export class SharedModule {}
    ```  
- **Use `forRoot` or `forChild`**: To configure shared services at the module level.  
- **Avoid Duplicates**: Ensure the shared module is imported once in the app module.  
- **Centralize Common Logic**: Include commonly used pipes or directives in the shared module.

---

### 10. **Difference Between AngularJS (1.x) and Angular (2.x and Beyond)?**  
- **Architecture**:  
  - AngularJS: MVC-based.  
  - Angular: Component-based architecture.  
- **Language**:  
  - AngularJS: JavaScript.  
  - Angular: TypeScript.  
- **Performance**:  
  - AngularJS: Two-way data binding caused performance issues.  
  - Angular: Unidirectional data flow and better change detection.  
- **Mobile Support**: Angular is optimized for mobile; AngularJS is not.  
- **Example**:  
  - AngularJS:  
    ```javascript
    app.controller('MainCtrl', function($scope) { $scope.message = 'Hello'; });
    ```  
  - Angular:  
    ```typescript
    @Component({
      selector: 'app-root',
      template: `<h1>{{ message }}</h1>`,
    })
    export class AppComponent {
      message = 'Hello';
    }
    ```  

---

### 11. **How to Break Down an E-Commerce Website into Modules and Components?**  
- **Feature Modules**: Create modules for key features like `ProductsModule`, `CartModule`, and `UserModule`.  
- **Shared Module**: Use a module for shared components like `NavbarComponent` and `FooterComponent`.  
- **Core Module**: For services like `AuthService` or `HttpInterceptor`.  
- **Example Structure**:  
  ```
  src/
  ├── app/
  │   ├── products/ (Product listing and details)
  │   ├── cart/ (Cart functionality)
  │   ├── user/ (Login, registration, profile)
  ```  
- **Components**:  
  - Product: `ProductListComponent`, `ProductDetailComponent`.  
  - Cart: `CartSummaryComponent`, `CheckoutComponent`.  

---

### 12. **How Does the Initialization of an Angular Application Happen?**  
- **Bootstrapping**: Angular starts with the `main.ts` file and calls the `platformBrowserDynamic` function.  
- **Root Module**: The `AppModule` is bootstrapped as the starting point.  
- **Root Component**: Defined in the `AppModule` using the `bootstrap` array.  
- **Example**:  
  ```typescript
  platformBrowserDynamic().bootstrapModule(AppModule);
  ```  
- **Modules and Components**: Angular initializes all imported modules and declared components in the root module.  

---

### 13. **What is the Purpose of the `@NgModule` Decorator, and What Are Its Key Sections?**  
- **Purpose**: Defines metadata for a module, including its components, services, and dependencies.  
- **Key Sections**:  
  - `declarations`: Components, directives, and pipes.  
  - `imports`: Other modules to include.  
  - `providers`: Services to use across the module.  
  - `bootstrap`: The root component to load initially.  
- **Example**:  
  ```typescript
  @NgModule({
    declarations: [AppComponent],
    imports: [BrowserModule],
    providers: [],
    bootstrap: [AppComponent],
  })
  export class AppModule {}
  ```  

---

### 14. **Can You Have Multiple `@NgModule` Decorators in an Angular Application?**  
- **Yes**, Angular applications can have multiple modules for organization.  
- **Feature Modules**: Define modules for specific functionalities (e.g., `UserModule`).  
- **Shared Module**: Used for reusable components and services.  
- **Core Module**: For single-instance services like `AuthService`.  
- **Example**:  
  - **AppModule**:  
    ```typescript
    @NgModule({
      imports: [UserModule],
    })
    export class AppModule {}
    ```  
  - **UserModule**:  
    ```typescript
    @NgModule({
      declarations: [UserProfileComponent],
    })
    export class UserModule {}
    ```  

---

### 15. **How to Add Modules in Angular?**  
- **Manually Import Modules**: Use the `imports` array in `@NgModule`.  
- **Add to AppModule**: Import built-in modules like `HttpClientModule` or custom modules.  
- **Lazy Loading**: Use the `loadChildren` property in the router for lazy-loaded modules.  
- **Example**:  
  - **Eager Loading**:  
    ```typescript
    @NgModule({
      imports: [BrowserModule, HttpClientModule],
    })
    export class AppModule {}
    ```  
  - **Lazy Loading**:  
    ```typescript
    const routes: Routes = [
      { path: 'products', loadChildren: () => import('./products/products.module').then(m => m.ProductsModule) },
    ];
    ```  

---

### 16. **How Does Angular Determine the Root Component for Bootstrapping?**  
- **Defined in AppModule**: The `bootstrap` array in `@NgModule` specifies the root component.  
- **AppComponent**: By default, `AppComponent` is the root component.  
- **Bootstrapping Process**:  
  1. `main.ts` calls `platformBrowserDynamic().bootstrapModule(AppModule)`.  
  2. Angular loads `AppComponent` to render the app.  
- **Example**:  
  ```typescript
  @NgModule({
    bootstrap: [AppComponent],
  })
  export class AppModule {}
  ```  
- **Root Element**: The component selector (e.g., `<app-root>`) must match the one in `index.html`.  

---

### 17. **What is the AppModule, and Why Is It Important?**  
- **Definition**: The root module of the application, which bootstraps the Angular app.  
- **Purpose**: Organizes the app by declaring components, importing modules, and providing services.  
- **Key Sections**:  
  - `declarations`: List of app-specific components, directives, and pipes.  
  - `imports`: Other modules needed for the app.  
  - `bootstrap`: Specifies the root component to render initially.  
- **Example**:  
  ```typescript
  @NgModule({
    declarations: [AppComponent],
    imports: [BrowserModule],
    bootstrap: [AppComponent],
  })
  export class AppModule {}
  ```  

---

### 18. **What is the Purpose of `enableProdMode()` in Angular, and When Should You Use It?**  
- **Purpose**: Disables Angular's development-specific checks for improved performance in production.  
- **When to Use**: Always enable it in production builds to reduce overhead.  
- **How to Enable**: Call `enableProdMode()` in the `main.ts` file.  
- **Example**:  
  ```typescript
  import { enableProdMode } from '@angular/core';
  if (environment.production) {
    enableProdMode();
  }
  platformBrowserDynamic().bootstrapModule(AppModule);
  ```  
- **Benefits**: Removes debug info and reduces runtime checks.  

---

### 19. **How Does Angular Handle Error Handling During the Bootstrapping Phase?**  
- **Global Error Handling**: Angular uses `ErrorHandler` for unhandled errors.  
- **Custom Error Handler**: You can override `ErrorHandler` to log or display custom messages.  
- **Errors During Bootstrapping**: Angular logs errors to the console if the app fails to bootstrap.  
- **Example**:  
  ```typescript
  export class MyErrorHandler implements ErrorHandler {
    handleError(error: any) {
      console.error('Custom Error:', error);
    }
  }
  @NgModule({
    providers: [{ provide: ErrorHandler, useClass: MyErrorHandler }],
  })
  export class AppModule {}
  ```  
- **Best Practices**: Use logging services to capture errors for debugging.  

---

### 20. **How to Implement Lazy Loading in Angular Using `@NgModule`?**  
- **Definition**: Lazy loading loads feature modules only when needed, reducing the initial app load time.  
- **Router Configuration**: Use `loadChildren` in the route definition.  
- **Steps**:  
  1. Create a feature module (e.g., `ProductsModule`).  
  2. Configure lazy loading in the route.  
  3. Ensure `RouterModule.forChild` is used in the feature module.  
- **Example**:  
  - **App Routing**:  
    ```typescript
    const routes: Routes = [
      { path: 'products', loadChildren: () => import('./products/products.module').then(m => m.ProductsModule) },
    ];
    ```  
  - **Products Module**:  
    ```typescript
    @NgModule({
      imports: [RouterModule.forChild(routes)],
    })
    export class ProductsModule {}
    ```  

---
### 21. **How to Configure Multiple Environments in Angular?**  
- **Purpose**: Manage different settings (e.g., API URLs) for development, staging, and production environments.  
- **Environment Files**: Angular uses `environment.ts` and `environment.prod.ts`.  
- **File Configuration**: Add properties specific to each environment.  
  - Example:  
    ```typescript
    // environment.ts
    export const environment = {
      production: false,
      apiUrl: 'http://localhost:3000',
    };
    // environment.prod.ts
    export const environment = {
      production: true,
      apiUrl: 'https://api.example.com',
    };
    ```  
- **Build Configuration**: Update `angular.json` to replace files based on the build environment.  
  - Example:  
    ```json
    "fileReplacements": [
      {
        "replace": "src/environments/environment.ts",
        "with": "src/environments/environment.prod.ts"
      }
    ]
    ```  

---

### 22. **What is the Difference Between `ng build` and `ng serve`?**  
- **`ng build`**:  
  - Compiles the app into static files for deployment.  
  - Generates output in the `dist/` folder.  
  - Can be used with `--prod` flag for optimized builds.  
- **`ng serve`**:  
  - Starts a local development server with live-reload.  
  - Does not generate build files in `dist/`.  
  - For development purposes only.  
- **Example Commands**:  
  - `ng build --prod`: Build for production.  
  - `ng serve --open`: Serve the app and open it in a browser.  

---

### 23. **What Are Decorators in Angular?**  
- **Definition**: Special functions in TypeScript that add metadata to classes, methods, or properties.  
- **Types of Decorators**:  
  - **Class Decorators**: `@Component`, `@Directive`, `@NgModule`.  
  - **Property Decorators**: `@Input`, `@Output`.  
  - **Method Decorators**: `@HostListener`, `@HostBinding`.  
- **Example**:  
  ```typescript
  @Component({
    selector: 'app-root',
    template: '<h1>Hello</h1>',
  })
  export class AppComponent {}
  ```  
- **Purpose**: Help Angular identify and configure components, directives, and services.  

---

### 24. **What is the Difference Between `@Component` and `@Directive` in Angular?**  
- **`@Component`**:  
  - Used to define a view (HTML template and associated logic).  
  - Example:  
    ```typescript
    @Component({
      selector: 'app-example',
      template: '<p>Component Template</p>',
    })
    export class ExampleComponent {}
    ```  
- **`@Directive`**:  
  - Adds behavior to existing elements without defining a view.  
  - Example:  
    ```typescript
    @Directive({
      selector: '[appHighlight]',
    })
    export class HighlightDirective {}
    ```  
- **Key Difference**: Components have templates, directives do not.

---

### 25. **What Are Directives in Angular?**  
- **Definition**: Instructions in Angular templates to extend HTML functionality.  
- **Types of Directives**:  
  - **Structural**: Change DOM structure (e.g., `*ngIf`, `*ngFor`).  
  - **Attribute**: Change behavior or appearance of elements (e.g., `ngClass`, `ngStyle`).  
  - **Custom**: User-defined directives.  
- **Example**:  
  - **Structural**:  
    ```html
    <div *ngIf="isVisible">Visible Content</div>
    ```  
  - **Attribute**:  
    ```html
    <div [ngStyle]="{ color: 'red' }">Styled Content</div>
    ```  

---

### 26. **What is the Difference Between Structural and Attribute Directives in Angular?**  
- **Structural Directives**:  
  - Modify the DOM structure by adding or removing elements.  
  - Example:  
    ```html
    <div *ngIf="isVisible">Content is visible</div>
    ```  
- **Attribute Directives**:  
  - Change the appearance or behavior of an element without altering its structure.  
  - Example:  
    ```html
    <div [ngStyle]="{ color: 'blue' }">Styled content</div>
    ```  
- **Key Difference**: Structural directives use `*`, attribute directives do not.  

---

### 27. **Have You Ever Created a Custom Directive? Can You Explain the Steps?**  
- **Steps to Create a Custom Directive**:  
  1. **Generate Directive**: Use the Angular CLI command: `ng generate directive highlight`.  
  2. **Add Metadata**: Define the directive selector in `@Directive`.  
  3. **Write Logic**: Add functionality inside the directive class.  
  - Example:  
    ```typescript
    @Directive({
      selector: '[appHighlight]',
    })
    export class HighlightDirective {
      constructor(private el: ElementRef) {
        this.el.nativeElement.style.backgroundColor = 'yellow';
      }
    }
    ```  
  4. **Use in Template**:  
    ```html
    <p appHighlight>Highlighted Text</p>
    ```  

---

### 28. **How Do You Use `@HostBinding` and `@HostListener` in Directives?**  
- **`@HostBinding`**: Binds a property to a host element.  
  - Example:  
    ```typescript
    @HostBinding('style.color') textColor = 'red';
    ```  
- **`@HostListener`**: Listens to events on the host element.  
  - Example:  
    ```typescript
    @HostListener('mouseenter') onMouseEnter() {
      this.textColor = 'blue';
    }
    @HostListener('mouseleave') onMouseLeave() {
      this.textColor = 'black';
    }
    ```  
- **Use Together**: Create interactive directives like hover effects.  

---

### 29. **What is Content Projection, and How Do You Implement It Using `ng-content`?**  
- **Definition**: Allows components to insert dynamic content into their templates.  
- **Implementation Steps**:  
  1. Add `<ng-content>` in the child component’s template.  
  - Example:  
    ```typescript
    @Component({
      selector: 'app-card',
      template: `<div class="card"><ng-content></ng-content></div>`,
    })
    export class CardComponent {}
    ```  
  2. Use the component in a parent template:  
    ```html
    <app-card>
      <p>Projected Content</p>
    </app-card>
    ```  
- **Output**: Displays "Projected Content" inside the card component.  

---

### 30. **How Do You Pass Data Between a Parent and a Child Component Using `@Input` and `@Output`?**  
- **`@Input`**: Pass data from parent to child.  
  - Example:  
    ```typescript
    @Input() title: string = '';
    ```  
    ```html
    <child-component [title]="'Hello'"></child-component>
    ```  
- **`@Output`**: Emit events from child to parent.  
  - Example:  
    ```typescript
    @Output() clicked = new EventEmitter<string>();
    onClick() {
      this.clicked.emit('Child clicked!');
    }
    ```  
    ```html
    <child-component (clicked)="handleClick($event)"></child-component>
    ```  
- **Communication**: Enables bidirectional data flow between components.  

---

### 31. **Explain the Difference Between `ngIf` and `[hidden]`.**  
- **`ngIf`**:  
  - Removes or adds the element from the DOM based on the condition.  
  - Example:  
    ```html
    <div *ngIf="isVisible">Visible Content</div>
    ```  
- **`[hidden]`**:  
  - Toggles the `hidden` attribute to hide or display the element without removing it from the DOM.  
  - Example:  
    ```html
    <div [hidden]="!isVisible">Visible Content</div>
    ```  
- **Key Difference**: `ngIf` improves performance by removing elements, while `[hidden]` retains them in the DOM.  

---

### 32. **What Is the Purpose of Angular Templates’ DOM Sanitization?**  
- **Definition**: Prevents Cross-Site Scripting (XSS) attacks by sanitizing unsafe inputs.  
- **Applied On**: Dynamically bound properties like `innerHTML` or URLs.  
- **Example**:  
  ```html
  <div [innerHTML]="userInput"></div>
  ```  
  - If `userInput` contains malicious scripts, Angular sanitizes it automatically.  
- **Bypass Security**: Use `DomSanitizer` if you trust the input.  
  ```typescript
  this.safeHtml = this.sanitizer.bypassSecurityTrustHtml(userInput);
  ```  

---

### 33. **What Are the Lifecycle Hooks for Components and Directives in Angular?**  
- **Common Lifecycle Hooks**:  
  1. **`ngOnInit`**: Initialization logic.  
  2. **`ngOnChanges`**: Responds to `@Input` changes.  
  3. **`ngDoCheck`**: Detects manual changes.  
  4. **`ngAfterViewInit`**: Executes after the component view initializes.  
  5. **`ngOnDestroy`**: Cleanup before the component is destroyed.  
- **Example**:  
  ```typescript
  ngOnInit() {
    console.log('Component initialized!');
  }
  ngOnDestroy() {
    console.log('Component destroyed!');
  }
  ```  

---

### 34. **What Are Dynamic Components in Angular?**  
- **Definition**: Components created at runtime rather than being statically declared.  
- **Use Case**: Displaying different components based on user actions.  
- **Steps to Implement**:  
  1. Use `ViewContainerRef` to specify the insertion point.  
  2. Use `ComponentFactoryResolver` to create components dynamically.  
- **Example**:  
  ```typescript
  this.vcr.createComponent(MyComponent);
  ```  

---

### 35. **How Do You Bind Data in Angular?**  
- **Types of Data Binding**:  
  1. **Interpolation**: Display data in templates.  
    ```html
    <h1>{{ title }}</h1>
    ```  
  2. **Property Binding**: Bind element properties.  
    ```html
    <input [value]="name" />
    ```  
  3. **Event Binding**: Listen to user events.  
    ```html
    <button (click)="onClick()">Click Me</button>
    ```  
  4. **Two-Way Binding**: Combine property and event binding.  
    ```html
    <input [(ngModel)]="name" />
    ```  
- **Purpose**: Synchronize data between the component and template.  

---

### 36. **What Is Angular’s Change Detection Strategy, and How Do You Manage Its Performance?**  
- **Change Detection**: Angular updates the DOM whenever data changes.  
- **Strategies**:  
  1. **Default**: Checks the entire component tree for changes.  
  2. **OnPush**: Checks only the component and its inputs.  
- **Performance Tips**:  
  - Use `OnPush` for immutable data.  
  - Avoid unnecessary bindings.  
  - Use `ChangeDetectorRef` to manually control detection.  
- **Example (OnPush)**:  
  ```typescript
  @Component({
    changeDetection: ChangeDetectionStrategy.OnPush,
  })
  ```  

---

### 37. **What Is the Role of `ChangeDetectorRef`, and How Do You Use It to Trigger or Detach Change Detection Manually?**  
- **Role**: Provides control over Angular's change detection.  
- **Methods**:  
  - `detectChanges()`: Manually triggers detection.  
  - `detach()`: Stops automatic detection for a component.  
- **Example**:  
  ```typescript
  constructor(private cdr: ChangeDetectorRef) {}
  updateView() {
    this.cdr.detectChanges();
  }
  ngOnInit() {
    this.cdr.detach();
  }
  ```  
- **Purpose**: Optimize performance in complex apps.  

---

### 38. **How Do You Use `OnPush` Change Detection for Performance Optimization?**  
- **Definition**: Updates the view only when component inputs change.  
- **Benefits**: Reduces unnecessary checks for unchanged data.  
- **Implementation**:  
  - Use `ChangeDetectionStrategy.OnPush` in the component decorator.  
- **Example**:  
  ```typescript
  @Component({
    changeDetection: ChangeDetectionStrategy.OnPush,
  })
  export class MyComponent {
    @Input() data: string;
  }
  ```  

---

### 39. **How Can You Handle Form Validation in Angular Using `ReactiveForms` and `TemplateDrivenForms`?**  
- **Reactive Forms**:  
  - Use `FormGroup` and `FormControl`.  
  - Example:  
    ```typescript
    this.form = new FormGroup({
      name: new FormControl('', [Validators.required]),
    });
    ```  
- **Template-Driven Forms**:  
  - Add validations directly in the template using directives.  
  - Example:  
    ```html
    <input [(ngModel)]="name" required />
    ```  
- **Error Handling**: Display validation messages using `ngIf`.  

---

### 40. **How Do You Create Custom Validators in Angular Reactive Forms?**  
- **Steps**:  
  1. Create a function that implements `ValidatorFn`.  
  2. Return an error object if validation fails, or `null` if it passes.  
  - Example:  
    ```typescript
    export function noSpecialChars(control: AbstractControl): ValidationErrors | null {
      const forbidden = /[^a-zA-Z0-9]/.test(control.value);
      return forbidden ? { noSpecialChars: true } : null;
    }
    ```  
  3. Apply the validator in `FormControl`:  
    ```typescript
    this.form = new FormControl('', [noSpecialChars]);
    ```  

---

### 41. **What Are `FormArray`s, and How Do You Use Them for Handling Dynamic Forms?**  
- **Definition**: A collection of `FormControl`, `FormGroup`, or other `FormArray` instances to manage dynamic form inputs.  
- **Use Case**: Add or remove fields dynamically in a form.  
- **Example**:  
  ```typescript
  this.form = new FormGroup({
    items: new FormArray([
      new FormControl('Item 1'),
    ]),
  });
  addItem() {
    (this.form.get('items') as FormArray).push(new FormControl(''));
  }
  ```  
  ```html
  <div *ngFor="let item of form.get('items').controls; let i = index">
    <input [formControl]="item" />
  </div>
  <button (click)="addItem()">Add Item</button>
  ```  

---

### 42. **What Are Template Reference Variables, and How Do You Use Them?**  
- **Definition**: Variables defined in templates to reference DOM elements or directives.  
- **Syntax**: Use `#` before the variable name.  
- **Example**:  
  ```html
  <input #myInput type="text" />
  <button (click)="logInput(myInput.value)">Log Input</button>
  ```  
  ```typescript
  logInput(value: string) {
    console.log(value);
  }
  ```  
- **Use Case**: Access elements or their properties in templates.  

---

### 43. **How Do You Use Angular’s `async` Pipe, and What Are Its Benefits?**  
- **Definition**: Unwraps `Observable` or `Promise` and binds the value to the template.  
- **Example**:  
  ```html
  <div *ngIf="data$ | async as data">
    {{ data }}
  </div>
  ```  
- **Benefits**:  
  - Automatically subscribes to and unsubscribes from observables.  
  - Simplifies handling asynchronous data.  

---

### 44. **What Is the Difference Between JIT and AOT Compilation in Angular?**  
- **Just-in-Time (JIT)**:  
  - Compiles templates in the browser at runtime.  
  - Faster during development but slower at runtime.  
  - Command: `ng serve` or `ng build`.  
- **Ahead-of-Time (AOT)**:  
  - Compiles templates at build time.  
  - Faster runtime performance and smaller bundles.  
  - Command: `ng build --prod`.  
- **Key Difference**: AOT improves performance and security by precompiling templates.  

---

### 45. **What Is the Purpose of `ViewChild` and `ViewChildren` in Angular?**  
- **`ViewChild`**: Access a single element or directive in the template.  
  - Example:  
    ```typescript
    @ViewChild('myInput') input: ElementRef;
    ngAfterViewInit() {
      console.log(this.input.nativeElement.value);
    }
    ```  
- **`ViewChildren`**: Access multiple elements or directives as a `QueryList`.  
  - Example:  
    ```typescript
    @ViewChildren('listItem') items: QueryList<ElementRef>;
    ngAfterViewInit() {
      this.items.forEach(item => console.log(item.nativeElement));
    }
    ```  

---

### 46. **Can You Explain Dependency Injection in Angular and How It Works?**  
- **Definition**: Design pattern where dependencies (services or objects) are provided to a class instead of being created by it.  
- **How It Works**:  
  - Define a service.  
  - Register the service in a module or with `@Injectable`.  
  - Inject the service into a component or directive via the constructor.  
- **Example**:  
  ```typescript
  @Injectable({ providedIn: 'root' })
  export class MyService {
    getData() {
      return 'Hello from Service';
    }
  }
  constructor(private myService: MyService) {
    console.log(myService.getData());
  }
  ```  

---

### 47. **What Is a Service, and When Would You Use It?**  
- **Definition**: A singleton class used to encapsulate business logic or data access.  
- **When to Use**:  
  - Share data across components.  
  - Encapsulate API calls.  
  - Handle reusable logic (e.g., authentication).  
- **Example**:  
  ```typescript
  @Injectable({ providedIn: 'root' })
  export class AuthService {
    login() {
      return 'Logged in';
    }
  }
  constructor(private authService: AuthService) {
    console.log(authService.login());
  }
  ```  

---

### 48. **What Is the Difference Between a Singleton Service and a Scoped Service in Angular?**  
- **Singleton Service**:  
  - A single instance shared across the entire app.  
  - Registered using `{ providedIn: 'root' }`.  
- **Scoped Service**:  
  - Separate instance created per module or component.  
  - Registered in the `providers` array of a module or component.  
- **Example**:  
  ```typescript
  @Injectable({ providedIn: 'root' }) // Singleton
  export class SharedService {}
  @NgModule({
    providers: [ScopedService], // Scoped
  })
  ```  

---

### 49. **How Does Angular’s Hierarchical Dependency Injection System Work?**  
- **Hierarchy Levels**:  
  1. **Root Injector**: Services provided at the app level.  
  2. **Module Injector**: Services provided in a specific module.  
  3. **Component Injector**: Services provided in a component.  
- **Behavior**:  
  - Child components can access services provided by parent injectors.  
  - Components have isolated instances if scoped providers are used.  
- **Example**:  
  ```typescript
  @Component({
    providers: [ScopedService],
  })
  ```  

---

### 50. **What Is the Difference Between `providedIn: 'root'` and `providedIn: 'any'` in Service Providers?**  
- **`providedIn: 'root'`**:  
  - Creates a singleton service at the app level.  
  - Recommended for most cases.  
- **`providedIn: 'any'`**:  
  - Creates a separate instance for each lazy-loaded module.  
- **Example**:  
  ```typescript
  @Injectable({ providedIn: 'root' }) // Singleton
  @Injectable({ providedIn: 'any' }) // Multiple instances
  ```  

---

### 51. **How Do You Provide a Service at the Component Level Instead of the Module Level?**  
- **Definition**: Providing a service at the component level creates an instance scoped to that component and its children.  
- **Steps**:  
  1. Add the service to the `providers` array of the component decorator.  
  - Example:  
    ```typescript
    @Component({
      selector: 'app-my-component',
      providers: [MyService],
    })
    export class MyComponent {
      constructor(private myService: MyService) {}
    }
    ```  
- **Behavior**: A new instance is created for each component.  

---

### 52. **How Do You Implement Optional Dependencies in Angular Using Dependency Injection?**  
- **Definition**: Optional dependencies are injected only if available; otherwise, `null` is used.  
- **Steps**:  
  1. Use the `@Optional()` decorator.  
  - Example:  
    ```typescript
    constructor(@Optional() private loggerService: LoggerService) {
      if (loggerService) {
        loggerService.log('Logger initialized.');
      }
    }
    ```  
- **Use Case**: Provide a fallback when a dependency is not available.  

---

### 53. **What Are Angular Injection Tokens, and When Should You Use Them?**  
- **Definition**: Tokens used to uniquely identify a dependency, especially for non-class providers like objects or strings.  
- **Steps to Use**:  
  1. Create a token using `InjectionToken`.  
  2. Provide the token in the `providers` array.  
  3. Inject the token in a constructor.  
- **Example**:  
  ```typescript
  const API_URL = new InjectionToken<string>('API_URL');
  @NgModule({
    providers: [{ provide: API_URL, useValue: 'https://api.example.com' }],
  })
  constructor(@Inject(API_URL) private apiUrl: string) {}
  ```  

---

### 54. **How Does Lazy Loading Work in Angular, and How Do You Implement It?**  
- **Definition**: Modules are loaded on demand rather than at the initial load, improving app performance.  
- **Steps to Implement**:  
  1. Create a separate module for the feature.  
  2. Use `loadChildren` in the `Routes` array.  
- **Example**:  
  ```typescript
  const routes: Routes = [
    { path: 'feature', loadChildren: () => import('./feature/feature.module').then(m => m.FeatureModule) },
  ];
  ```  

---

### 55. **What Are Route Guards in Angular, and How Do You Implement Them for Authentication?**  
- **Definition**: Guards control access to routes based on logic like authentication or authorization.  
- **Steps to Implement**:  
  1. Create a guard using `ng generate guard`.  
  2. Implement the `CanActivate` interface.  
  3. Add the guard to the route configuration.  
- **Example**:  
  ```typescript
  @Injectable({ providedIn: 'root' })
  export class AuthGuard implements CanActivate {
    canActivate(): boolean {
      return this.authService.isLoggedIn();
    }
  }
  const routes: Routes = [{ path: 'dashboard', canActivate: [AuthGuard], component: DashboardComponent }];
  ```  

### 56. **What Are the Different Types of Angular Guards (`CanActivate`, `CanDeactivate`, etc.)?**  
- **`CanActivate`**: Determines if a route can be activated.  
  - Example:  
    ```typescript
    @Injectable({ providedIn: 'root' })
    export class AuthGuard implements CanActivate {
      canActivate(): boolean {
        return this.authService.isLoggedIn();
      }
    }
    ```  
- **`CanDeactivate`**: Checks if a route can be exited (useful for unsaved changes).  
  - Example:  
    ```typescript
    export class UnsavedChangesGuard implements CanDeactivate<unknown> {
      canDeactivate(): boolean {
        return confirm('Do you want to leave this page?');
      }
    }
    ```  
- **`Resolve`**: Pre-fetches data before activating a route.  
- **`CanLoad`**: Prevents modules from loading unless criteria are met.  
- **`CanActivateChild`**: Checks access for child routes.  

---

### 57. **How Do You Implement Role-Based Access Control in Angular Routing?**  
- **Definition**: Restrict routes based on user roles.  
- **Steps to Implement**:  
  1. Add roles to user objects (e.g., `['admin', 'user']`).  
  2. Use a `CanActivate` guard to check roles.  
  - Example:  
    ```typescript
    canActivate(route: ActivatedRouteSnapshot): boolean {
      const expectedRole = route.data.role;
      return this.authService.hasRole(expectedRole);
    }
    const routes: Routes = [
      { path: 'admin', component: AdminComponent, canActivate: [RoleGuard], data: { role: 'admin' } },
    ];
    ```  

---

### 58. **How Do You Resolve Data Before Activating a Route in Angular?**  
- **Definition**: Use `Resolve` guards to fetch data before navigating to a route.  
- **Steps to Implement**:  
  1. Create a resolver service implementing `Resolve<T>`.  
  2. Use it in the route’s `resolve` property.  
  - Example:  
    ```typescript
    @Injectable({ providedIn: 'root' })
    export class DataResolver implements Resolve<any> {
      resolve(): Observable<any> {
        return this.dataService.getData();
      }
    }
    const routes: Routes = [
      { path: 'details', component: DetailsComponent, resolve: { data: DataResolver } },
    ];
    ```  

---

### 59. **How Do You Handle Preloading Strategies in Angular for Performance Optimization?**  
- **Definition**: Preload lazy-loaded modules in the background to improve perceived performance.  
- **Built-In Strategies**:  
  1. **NoPreloading**: Default, does not preload modules.  
  2. **PreloadAllModules**: Preloads all lazy-loaded modules.  
- **Steps to Use**:  
  - Enable preloading in `RouterModule`:  
    ```typescript
    RouterModule.forRoot(routes, { preloadingStrategy: PreloadAllModules });
    ```  
- **Custom Strategies**: Create custom logic to decide which modules to preload.  

---

### 60. **What Is the Difference Between `routerLink` and `routerLinkActive`?**  
- **`routerLink`**: Specifies the route to navigate to when clicked.  
  - Example:  
    ```html
    <a routerLink="/home">Home</a>
    ```  
- **`routerLinkActive`**: Applies a CSS class when the route is active.  
  - Example:  
    ```html
    <a routerLink="/home" routerLinkActive="active">Home</a>
    ```  
- **Key Difference**: `routerLink` navigates, while `routerLinkActive` highlights the active route.  

---

### 61. **How Do You Detect Route Changes in Angular?**  
- **Using `Router` Events**: Subscribe to the `Router`’s `events` observable.  
  - Example:  
    ```typescript
    constructor(private router: Router) {
      this.router.events.subscribe(event => {
        if (event instanceof NavigationEnd) {
          console.log('Route changed to:', event.url);
        }
      });
    }
    ```  
- **Using `ActivatedRoute`**: Access `paramMap` or `url` observables for route parameter changes.  
  - Example:  
    ```typescript
    constructor(private route: ActivatedRoute) {
      this.route.paramMap.subscribe(params => {
        console.log('Route parameter:', params.get('id'));
      });
    }
    ```  

---

### 62. **What Is the Purpose of a Wildcard Route in Angular?**  
- **Definition**: A fallback route for undefined paths, typically used for 404 pages.  
- **Syntax**:  
  ```typescript
  const routes: Routes = [
    { path: '**', component: NotFoundComponent },
  ];
  ```  
- **Behavior**: Matches any route not explicitly defined in the `Routes` array.  

---

### 63. **What Is Router State, and How Do You Manage It?**  
- **Definition**: Represents the current state of the router, including active routes and parameters.  
- **Accessing Router State**:  
  - Use `Router` to navigate or inspect the current URL.  
  - Example:  
    ```typescript
    const currentUrl = this.router.url;
    console.log('Current URL:', currentUrl);
    ```  
- **Managing State**: Use route guards, resolvers, or services to manage navigation logic.  

---

### 64. **How Do You Handle Forms in Angular (Template-Driven vs. Reactive)?**  
- **Template-Driven Forms**:  
  - Use Angular directives like `ngModel`.  
  - Easier for simple forms.  
  - Example:  
    ```html
    <form #form="ngForm">
      <input [(ngModel)]="name" name="name" required />
    </form>
    ```  
- **Reactive Forms**:  
  - Use `FormGroup` and `FormControl` for better control.  
  - Example:  
    ```typescript
    this.form = new FormGroup({
      name: new FormControl('', Validators.required),
    });
    ```  

---

### 65. **What Is the Purpose of `FormBuilder` and `FormGroup`, and How Do You Use Them?**  
- **`FormBuilder`**: Simplifies creating reactive forms.  
- **`FormGroup`**: Groups related form controls.  
- **Example**:  
  ```typescript
  constructor(private fb: FormBuilder) {
    this.form = this.fb.group({
      name: ['', Validators.required],
      email: ['', Validators.email],
    });
  }
  ```  

---

### 66. **How Do You Reset a Form in Angular Without Losing Validation?**  
- **Using `reset()`**: Resets form fields and retains validation rules.  
  - Example:  
    ```typescript
    this.form.reset();
    ```  
- **Passing Default Values**: Use `reset()` with a value object.  
  - Example:  
    ```typescript
    this.form.reset({ name: 'Default Name', email: '' });
    ```  
- **Handling Nested Form Groups**: Ensure nested controls are reset properly.  
  - Example:  
    ```typescript
    this.form.get('address').reset();
    ```  

---

### 67. **What Is the Role of `NgModel` in Template-Driven Forms?**  
- **Purpose**: Binds form inputs to model properties.  
- **Two-Way Data Binding**: Uses `[(ngModel)]` for synchronization.  
  - Example:  
    ```html
    <input [(ngModel)]="username" name="username" required />
    ```  
- **Form Control Integration**: Links controls with `NgForm`.  

---

### 68. **How Do You Add Dynamic Validation to Angular Reactive Form Controls?**  
- **Adding Validators Dynamically**: Use `setValidators` or `addValidators`.  
  - Example:  
    ```typescript
    this.form.get('email').setValidators([Validators.required, Validators.email]);
    this.form.get('email').updateValueAndValidity();
    ```  
- **Removing Validators**: Use `clearValidators` and update validity.  
  - Example:  
    ```typescript
    this.form.get('email').clearValidators();
    this.form.get('email').updateValueAndValidity();
    ```  

---

### 69. **What Are the Utility Functions Provided by RxJS?**  
- **Key Utility Operators**:  
  - `map`: Transform data in a stream.  
    ```typescript
    of(1, 2, 3).pipe(map(x => x * 2)).subscribe(console.log);
    ```  
  - `filter`: Filter items based on a condition.  
    ```typescript
    of(1, 2, 3).pipe(filter(x => x > 1)).subscribe(console.log);
    ```  
  - `mergeMap`: Flatten and merge inner observables.  
  - `debounceTime`: Delay stream emissions to avoid rapid firing.  

---

### 70. **How Do You Manage Complex Streams of Asynchronous Data Using RxJS?**  
- **Combining Streams**: Use operators like `merge`, `combineLatest`, or `forkJoin`.  
  - Example:  
    ```typescript
    combineLatest([stream1, stream2]).subscribe(([val1, val2]) => {
      console.log(val1, val2);
    });
    ```  
- **Error Handling**: Use `catchError` and `retry`.  
  - Example:  
    ```typescript
    http.get('url').pipe(catchError(err => of('Fallback data')));
    ```  
- **State Management**: Use `BehaviorSubject` or `ReplaySubject` for state-like behavior.  

---

Would you like the next set of questions or further details on these topics?### 71. **What Are Advanced RxJS Operators Like `switchMap`, `concatMap`, and `exhaustMap`, and How Are They Used in Angular?**  
- **`switchMap`**: Switches to a new observable, canceling previous emissions. Useful for search or typeahead scenarios.  
  - Example:  
    ```typescript
    this.searchInput.valueChanges.pipe(
      debounceTime(300),
      switchMap(query => this.searchService.search(query))
    ).subscribe(results => console.log(results));
    ```  
- **`concatMap`**: Executes observables sequentially, ensuring the order. Useful for tasks requiring order.  
  - Example:  
    ```typescript
    this.taskQueue.pipe(concatMap(task => this.taskService.process(task))).subscribe();
    ```  
- **`exhaustMap`**: Ignores new emissions while a previous observable is still active. Useful for forms to prevent duplicate submissions.  
  - Example:  
    ```typescript
    this.formSubmit.pipe(
      exhaustMap(() => this.authService.submitForm(this.form.value))
    ).subscribe();
    ```  

---

### 72. **How Do You Use Operators Like `catchError` and `retry` for HTTP Requests in Angular?**  
- **`catchError`**: Handles errors in an observable.  
  - Example:  
    ```typescript
    this.http.get('/api/data').pipe(
      catchError(err => of({ error: true, message: err.message }))
    ).subscribe(data => console.log(data));
    ```  
- **`retry`**: Retries a failed observable a specified number of times.  
  - Example:  
    ```typescript
    this.http.get('/api/data').pipe(
      retry(3),
      catchError(err => throwError(() => new Error('Failed after 3 retries')))
    ).subscribe();
    ```  

---

### 73. **What Is the Purpose of the `tap` Operator in RxJS?**  
- **Definition**: Performs side effects like logging or debugging without altering the stream.  
- **Example**:  
  ```typescript
  this.http.get('/api/data').pipe(
    tap(data => console.log('Received data:', data))
  ).subscribe();
  ```  
- **Use Case**: Logging, debugging, or triggering auxiliary actions without modifying values.  

---

### 74. **Explain `forkJoin` in RxJS with an Example.**  
- **Definition**: Combines multiple observables, emitting their final values as an array.  
- **Example**:  
  ```typescript
  forkJoin([
    this.http.get('/api/user'),
    this.http.get('/api/orders')
  ]).subscribe(([user, orders]) => {
    console.log('User:', user);
    console.log('Orders:', orders);
  });
  ```  
- **Use Case**: Execute multiple independent observables and wait for all to complete.  

---

### 75. **What Is Debounce, and Why Do We Use It in Angular?**  
- **Definition**: Delays observable emissions until a specified period of inactivity.  
- **Use Case**: Prevent rapid firing of events like keystrokes.  
- **Example**:  
  ```typescript
  this.searchInput.valueChanges.pipe(
    debounceTime(300),
    distinctUntilChanged(),
    switchMap(query => this.searchService.search(query))
  ).subscribe(results => console.log(results));
  ```  
- **Benefit**: Optimizes performance by reducing unnecessary calls.  

---

### 76. **How Do You Cancel a Pending HTTP Request in Angular Using RxJS?**  
- **Use `takeUntil` with a `Subject`**: Emits and completes an observable to cancel the request.  
  - Example:  
    ```typescript
    private destroy$ = new Subject<void>();
    this.http.get('/api/data').pipe(
      takeUntil(this.destroy$)
    ).subscribe();
    // Cancel the request
    this.destroy$.next();
    this.destroy$.complete();
    ```  
- **Use `AbortController` (Angular 16+ with Fetch API)**: Abort ongoing requests.  
  - Example:  
    ```typescript
    const controller = new AbortController();
    this.http.get('/api/data', { signal: controller.signal }).subscribe();
    controller.abort(); // Cancels the request
    ```  

---

### 77. **What Is NGRX, and How Do You Use It for State Management in Angular?**  
- **Definition**: A reactive state management library using the Redux pattern.  
- **Core Elements**:  
  - **Store**: Centralized state container.  
  - **Actions**: Dispatchable events to change the state.  
  - **Reducers**: Pure functions to handle state changes.  
  - **Selectors**: Retrieve specific state slices.  
- **Example**:  
  ```typescript
  // Action
  export const increment = createAction('[Counter] Increment');
  // Reducer
  const counterReducer = createReducer(0, on(increment, state => state + 1));
  // Component
  this.store.dispatch(increment());
  this.store.select('counter').subscribe(console.log);
  ```  

---

### 78. **How Do You Handle Side Effects in NGRX Using Effects?**  
- **Purpose**: To handle external interactions like API calls without directly modifying the store.  
- **Example**:  
  ```typescript
  @Injectable()
  export class CounterEffects {
    loadData$ = createEffect(() => this.actions$.pipe(
      ofType(loadData),
      mergeMap(() => this.apiService.getData().pipe(
        map(data => loadDataSuccess({ data })),
        catchError(() => of(loadDataFailure()))
      ))
    ));
    constructor(private actions$: Actions, private apiService: ApiService) {}
  }
  ```  

---

### 79. **How Do You Use NGRX Selectors for Better State Querying?**  
- **Purpose**: Simplifies and memoizes state queries.  
- **Create Selector**:  
  - Example:  
    ```typescript
    const selectFeature = (state: AppState) => state.feature;
    const selectFeatureItems = createSelector(selectFeature, feature => feature.items);
    this.store.select(selectFeatureItems).subscribe(console.log);
    ```  
- **Composition**: Combine selectors for nested or derived data.  

---

### 80. **What Is the Purpose of Immutability in State Management, and How Do You Enforce It?**  
- **Purpose**: Prevents accidental state mutations, ensuring predictable behavior.  
- **Enforcement in NGRX**:  
  - Use immutability helpers like `createReducer` and `on`.  
  - Avoid mutating state directly in reducers.  
- **Immutable Libraries**: Use libraries like `immer` for complex structures.  
  - Example:  
    ```typescript
    const newState = produce(oldState, draft => {
      draft.items.push(newItem);
    });
    ```  

---

### 81. **How Do You Manage Local Component State Versus Global Application State in Angular?**  
- **Local Component State**:  
  - Stored directly in the component for UI-specific needs.  
  - Example:  
    ```typescript
    export class MyComponent {
      localState = { isActive: false };
    }
    ```  
- **Global Application State**:  
  - Managed using services or state management libraries like NGRX.  
  - Example:  
    ```typescript
    this.store.select('globalState').subscribe(data => console.log(data));
    ```  
- **Decision**: Use local state for isolated components and global state for shared data or cross-component communication.  

---

### 82. **How Do You Handle HTTP Requests in Angular Using the `HttpClientModule`?**  
- **Steps**:  
  1. Import `HttpClientModule` in `AppModule`.  
  2. Inject `HttpClient` service into a component or service.  
  3. Use HTTP methods like `get`, `post`, `put`, and `delete`.  
  - Example:  
    ```typescript
    this.http.get('/api/items').subscribe(data => console.log(data));
    ```  
- **Use Cases**: Fetch data, send form data, and delete resources.  

---

### 83. **How Do You Implement Interceptors for Modifying Outgoing HTTP Requests?**  
- **Definition**: Interceptors allow you to inspect or modify HTTP requests or responses globally.  
- **Implementation**:  
  1. Create a service implementing `HttpInterceptor`.  
  2. Modify the `req` or handle `res`.  
  - Example:  
    ```typescript
    export class AuthInterceptor implements HttpInterceptor {
      intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
        const authReq = req.clone({ headers: req.headers.set('Authorization', 'Bearer token') });
        return next.handle(authReq);
      }
    }
    ```  
  3. Provide it in `AppModule` with `HTTP_INTERCEPTORS`.  

---

### 84. **How Do You Handle Error Handling for HTTP Requests in a Centralized Manner?**  
- **Approaches**:  
  - **Use Interceptors**: Catch and handle errors globally.  
    ```typescript
    export class ErrorInterceptor implements HttpInterceptor {
      intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
        return next.handle(req).pipe(
          catchError(err => {
            console.error('Error intercepted:', err);
            return throwError(() => new Error(err.message));
          })
        );
      }
    }
    ```  
  - **Central Error Service**: Create a service to manage error logs or user notifications.  

---

### 85. **What Is the Role of `HttpParams` in Angular HTTP Requests?**  
- **Definition**: Used for adding query parameters to HTTP requests.  
- **Example**:  
  ```typescript
  const params = new HttpParams().set('page', '1').set('limit', '10');
  this.http.get('/api/items', { params }).subscribe();
  ```  
- **Benefits**:  
  - Cleaner URL construction.  
  - Helps with dynamic query parameter addition.  

---

### 86. **How Do You Handle Retry Logic for Failed HTTP Requests in Angular?**  
- **Using `retry` Operator**: Automatically retry failed requests a specified number of times.  
  - Example:  
    ```typescript
    this.http.get('/api/data').pipe(
      retry(3),
      catchError(err => {
        console.error('Request failed:', err);
        return throwError(() => new Error('Retry failed'));
      })
    ).subscribe();
    ```  
- **Using `retryWhen`**: Retry based on custom logic (e.g., exponential backoff).  
  - Example:  
    ```typescript
    this.http.get('/api/data').pipe(
      retryWhen(errors => errors.pipe(delay(1000), take(3)))
    ).subscribe();
    ```  

---

### 87. **How Do You Test Angular Components Using Karma and Jasmine?**  
- **Steps**:  
  1. Generate the component test file using Angular CLI (`.spec.ts`).  
  2. Import required modules and dependencies in `TestBed`.  
  - Example:  
    ```typescript
    beforeEach(() => {
      TestBed.configureTestingModule({
        declarations: [MyComponent],
        imports: [HttpClientTestingModule],
      }).compileComponents();
    });
    ```  
  3. Write unit tests for component behavior using `it`.  
  - Example:  
    ```typescript
    it('should create the component', () => {
      const fixture = TestBed.createComponent(MyComponent);
      const app = fixture.componentInstance;
      expect(app).toBeTruthy();
    });
    ```  

---

### 88. **How Do You Generate a Coverage Report in Angular Tests?**  
- **Steps to Generate**:  
  1. Run tests with coverage:  
     ```bash
     ng test --code-coverage
     ```  
  2. Navigate to the `coverage` folder generated in the project directory.  
  3. Open `index.html` in a browser for detailed reports.  
- **Usage**: Identifies untested parts of the application.  

---

### 89. **How Do You Mock Services for Testing in Angular?**  
- **Using Jasmine Spies**: Replace service methods with mock implementations.  
  - Example:  
    ```typescript
    const mockService = jasmine.createSpyObj('MyService', ['getData']);
    mockService.getData.and.returnValue(of(mockData));
    ```  
- **Using `HttpClientTestingModule`**: Mock HTTP requests.  
  - Example:  
    ```typescript
    TestBed.configureTestingModule({
      providers: [MyService],
      imports: [HttpClientTestingModule]
    });
    ```  

---

### 90. **What Are Angular `TestBed` Utilities, and How Do You Use Them?**  
- **Purpose**: Configure and initialize the Angular testing environment.  
- **Key Features**:  
  - `configureTestingModule`: Sets up module dependencies.  
  - `createComponent`: Instantiates components.  
  - Example:  
    ```typescript
    TestBed.configureTestingModule({
      declarations: [MyComponent],
      imports: [HttpClientTestingModule]
    }).compileComponents();
    ```  
- **Use Case**: Unit testing for components, services, and directives.  

---

### 91. **How Do You Debug an Angular Application or a Lazy-Loaded Module?**  
- **Use Angular DevTools**: A Chrome extension for inspecting Angular applications.  
- **Enable Source Maps**: Add `"sourceMap": true` in `angular.json` for debugging TypeScript in browsers.  
- **Console Logging**: Use `console.log` or `debugger` to inspect variables.  
- **Debug Lazy-Loaded Modules**:  
  - Check `RouterModule.forChild` configuration.  
  - Verify module paths in `loadChildren`.  
  - Example:  
    ```typescript
    RouterModule.forRoot([
      { path: 'lazy', loadChildren: () => import('./lazy/lazy.module').then(m => m.LazyModule) }
    ])
    ```  

---

### 92. **How Do You Test a Component That Uses Angular Material?**  
- **Import Material Modules**: Import required Material modules in the test.  
  - Example:  
    ```typescript
    TestBed.configureTestingModule({
      declarations: [MaterialComponent],
      imports: [MatButtonModule, MatDialogModule]
    }).compileComponents();
    ```  
- **Use `Harness` for Testing**: Use Angular Material test harness for robust testing.  
  - Example:  
    ```typescript
    const loader = TestbedHarnessEnvironment.loader(fixture);
    const button = await loader.getHarness(MatButtonHarness);
    await button.click();
    ```  

---

### 93. **How Do You Optimize the Performance of an Angular Application?**  
- **Use OnPush Change Detection**: Minimizes unnecessary component checks.  
- **Lazy Load Modules**: Load only required modules on demand.  
- **Tree-Shaking**: Ensure unused code is removed during build.  
- **Optimize Template Rendering**:  
  - Use `trackBy` in `ngFor`.  
  - Example:  
    ```typescript
    <div *ngFor="let item of items; trackBy: trackByFn"></div>
    ```  
- **Bundle Optimization**: Use `ng build --prod`.  

---

### 94. **What Are Some Key Performance Bottlenecks in Angular, and How Do You Address Them?**  
- **Excessive Change Detection**: Use `ChangeDetectionStrategy.OnPush`.  
- **Large Initial Bundle Size**:  
  - Use lazy loading for modules.  
  - Enable code splitting with dynamic imports.  
- **Inefficient DOM Updates**: Use `trackBy` for lists and `ngIf` for conditional rendering.  
- **Multiple HTTP Calls**: Use `forkJoin` or caching mechanisms.  

---

### 95. **How Do You Use `trackBy` in `ngFor` to Improve Performance?**  
- **Purpose**: Reduces DOM re-rendering by identifying changes using a unique key.  
- **Implementation**:  
  - Add a `trackBy` function in the component.  
  - Example:  
    ```typescript
    trackByFn(index: number, item: any): number {
      return item.id; // or unique key
    }
    ```  
  - Use it in the template:  
    ```html
    <div *ngFor="let item of items; trackBy: trackByFn">{{ item.name }}</div>
    ```  

---
### 96. **How Does Angular Optimize HTTP Requests with Caching?**  
- **Using Interceptors**: Cache responses globally to avoid redundant requests.  
  - Example:  
    ```typescript
    intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
      const cachedResponse = this.cache.get(req.url);
      return cachedResponse ? of(cachedResponse) : next.handle(req).pipe(
        tap(event => {
          if (event instanceof HttpResponse) {
            this.cache.set(req.url, event);
          }
        })
      );
    }
    ```  
- **HTTP Headers**: Use caching headers like `ETag` or `Cache-Control`.  
- **Service Layer Caching**: Store frequently accessed data in a service variable.  

---

### 97. **How Do You Implement Lazy Loading of Images in Angular?**  
- **Using `loading="lazy"` Attribute**: Add to image tags for native lazy loading.  
  - Example:  
    ```html
    <img src="image.jpg" alt="example" loading="lazy" />
    ```  
- **Using Directives**: Create a custom directive to load images when in the viewport.  
  - Example:  
    ```typescript
    @Directive({ selector: '[lazyLoad]' })
    export class LazyLoadDirective {
      @HostBinding('attr.src') srcAttr = null;
      @Input('lazyLoad') set lazyLoad(src: string) {
        const observer = new IntersectionObserver(([entry]) => {
          if (entry.isIntersecting) {
            this.srcAttr = src;
            observer.disconnect();
          }
        });
        observer.observe(this.element.nativeElement);
      }
    }
    ```  

---

### 98. **What Are Best Practices for Optimizing Large Forms in Angular?**  
- **Lazy Loading Form Modules**: Split forms into smaller, lazy-loaded modules.  
- **OnPush Change Detection**: Reduce unnecessary checks.  
- **Use `FormArray` for Dynamic Fields**: Manage large dynamic inputs efficiently.  
  - Example:  
    ```typescript
    this.form = this.fb.group({
      items: this.fb.array([])
    });
    ```  
- **Debounce Validation**: Minimize frequent validations with `debounceTime`.  
  - Example:  
    ```typescript
    this.form.valueChanges.pipe(debounceTime(300)).subscribe();
    ```  

---

### 99. **How Does Angular Prevent XSS Attacks, and What Are Best Practices for Securing Templates?**  
- **Built-in Sanitization**: Automatically sanitizes HTML, URLs, and styles.  
- **Avoid `innerHTML`**: Use Angular bindings instead of directly setting HTML.  
- **Sanitize with `DomSanitizer`**: Explicitly mark trusted content.  
  - Example:  
    ```typescript
    this.safeHtml = this.sanitizer.bypassSecurityTrustHtml('<b>Safe Content</b>');
    ```  
- **Use `strictTemplatePolicy`**: Enable strict template checks in `tsconfig.json`.  

---

### 100. **How Do You Handle CSRF Tokens in Angular Applications?**  
- **Set CSRF Token in Request Headers**: Send tokens with every HTTP request.  
  - Example:  
    ```typescript
    intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
      const token = this.csrfService.getToken();
      const cloned = req.clone({ headers: req.headers.set('X-CSRF-Token', token) });
      return next.handle(cloned);
    }
    ```  
- **Use Secure Cookies**: Store tokens in `HttpOnly` cookies to avoid client-side tampering.  
- **Validate on Server Side**: Ensure tokens are validated for each request.  

---

### 101. **How Do You Implement OAuth2 Authentication in Angular?**  
- **Integrate OAuth2 Library**: Use libraries like `angular-oauth2-oidc`.  
  - Example:  
    ```typescript
    this.oauthService.configure({
      clientId: 'client-id',
      issuer: 'https://auth-server.com',
      redirectUri: window.location.origin,
      responseType: 'code',
      scope: 'openid profile email'
    });
    this.oauthService.loadDiscoveryDocumentAndTryLogin();
    ```  
- **Handle Tokens**: Store the access token securely (e.g., in memory or `HttpOnly` cookies).  
- **Guard Routes**: Use `AuthGuard` to protect routes.  
  - Example:  
    ```typescript
    { path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] }
    ```  

---

### 102. **What Is the Role of HTTP Interceptors in Securing API Calls?**  
- **Add Authorization Headers**: Automatically attach tokens to API calls.  
  - Example:  
    ```typescript
    intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
      const token = this.authService.getToken();
      const cloned = req.clone({ headers: req.headers.set('Authorization', `Bearer ${token}`) });
      return next.handle(cloned);
    }
    ```  
- **Handle Errors**: Redirect to login on `401 Unauthorized`.  
- **Log API Calls**: Track or debug HTTP traffic.  

---

### 103. **How Do You Implement Content Security Policy (CSP) with Angular?**  
- **Define CSP Headers**: Add headers in the server configuration.  
  - Example (Nginx):  
    ```nginx
    Content-Security-Policy: default-src 'self'; script-src 'self' 'nonce-abc123';
    ```  
- **Nonce for Scripts**: Dynamically generate and attach a nonce to inline scripts.  
- **Sanitize Dynamic Content**: Use Angular's `DomSanitizer` to ensure content adheres to CSP.  

---

### 104. **What Is Angular Universal, and How Do You Implement Server-Side Rendering (SSR)?**  
- **Definition**: Angular Universal enables server-side rendering (SSR) for better SEO and faster load times.  
- **Steps to Implement**:  
  1. Install Universal:  
     ```bash
     ng add @nguniversal/express-engine
     ```  
  2. Build SSR Application:  
     ```bash
     npm run build:ssr
     ```  
  3. Serve with Node.js:  
     ```bash
     npm run serve:ssr
     ```  
  - Example: Pre-rendered content for SEO bots.

---

### 105. **How Do You Cache Data in SSR for Performance Improvements?**  
- **Server-Side Caching**: Cache rendered pages at the server level (e.g., Redis or CDN).  
- **Angular Transfer State**: Share API responses between SSR and client.  
  - Example:  
    ```typescript
    import { TransferState, makeStateKey } from '@angular/platform-browser';
    const DATA_KEY = makeStateKey<any>('cachedData');
    
    this.state.set(DATA_KEY, fetchedData);
    const cachedData = this.state.get(DATA_KEY, null);
    ```  
- **Service Worker Caching**: Use Angular’s PWA capabilities to cache assets and API calls.  

--- 

### 106. **What Are Common Challenges in Implementing SSR with Angular, and How Do You Overcome Them?**  
- **Challenge: Third-Party Libraries**: Some libraries depend on browser-specific APIs (e.g., `window` or `document`).  
  - **Solution**: Use `isPlatformBrowser` to conditionally run code.  
  - Example:  
    ```typescript
    if (isPlatformBrowser(this.platformId)) {
      // Browser-specific code
    }
    ```  
- **Challenge: State Transfer**: Data fetched during SSR isn't shared with the client.  
  - **Solution**: Use Angular's `TransferState` module to share data between server and client.  
- **Challenge: Large Initial Payload**: SSR may send large HTML files.  
  - **Solution**: Optimize lazy loading and use compression (e.g., Gzip).  

---

### 107. **What Is the Ivy Renderer, and How Does It Differ from the Previous View Engine?**  
- **Definition**: Ivy is Angular’s next-generation rendering engine, introduced in Angular 9.  
- **Differences from View Engine**:  
  - **Faster Compilation**: Compiles components to highly optimized JavaScript.  
  - **Smaller Bundle Size**: Implements tree-shaking to remove unused code.  
  - **Improved Debugging**: Better error messages and stack traces.  
  - Example: Ivy allows dynamic component rendering using `createComponent`.  

---

### 108. **What Is `ng-template` vs. `ng-container` in Angular?**  
- **`ng-template`**: Used to define reusable template content.  
  - Example:  
    ```html
    <ng-template #templateRef><p>Template Content</p></ng-template>
    <ng-container *ngTemplateOutlet="templateRef"></ng-container>
    ```  
- **`ng-container`**: Acts as a logical grouping element without adding extra DOM.  
  - Example:  
    ```html
    <ng-container *ngIf="isVisible">
      <p>Conditionally Rendered</p>
    </ng-container>
    ```  
- **Key Difference**: `ng-template` is for templates, while `ng-container` is for grouping without extra DOM.

---

### 109. **How Does Angular Handle Tree-Shaking to Reduce Bundle Size Using Ivy?**  
- **Tree-Shaking Defined**: Removes unused code during build time.  
- **Mechanisms in Ivy**:  
  - **Component-Level Code Splitting**: Compiles components into independent functions.  
  - **Dead Code Elimination**: Removes unused services, pipes, or directives.  
- **Example**: If a pipe isn’t used, it’s excluded from the final bundle.  
  - **Tools**: `ng build --prod` leverages Webpack for tree-shaking.  

---

### 110. **What Is Differential Loading in Angular?**  
- **Definition**: Angular generates two bundles: one for modern browsers (ES2015) and another for older ones (ES5).  
- **Advantages**:  
  - Smaller, faster bundles for modern browsers.  
  - Compatibility with older browsers.  
- **Configuration**: Angular CLI automatically handles it during production builds.  
  - Example:  
    ```json
    "browserslist": ["last 2 versions", "not dead", "IE 11"]
    ```  

---  

### 111. **How Do You Configure Angular for Microservices Architectures?**  
- **Separate Modules for Each Feature**: Create Angular modules corresponding to each microservice.  
  - Example:  
    ```typescript
    const routes: Routes = [
      { path: 'user', loadChildren: () => import('./user/user.module').then(m => m.UserModule) },
      { path: 'order', loadChildren: () => import('./order/order.module').then(m => m.OrderModule) },
    ];
    ```  
- **API Gateway**: Use a centralized service for communication with microservices.  
- **Shared Module**: Create a shared library for common utilities (e.g., models, services).  
- **Environment-Specific Configurations**: Use `environment.ts` for different microservice URLs.  

---

### 112. **How Do You Dynamically Load External Modules in Angular?**  
- **Use Angular’s `loadChildren` Syntax**: Load modules lazily at runtime.  
  - Example:  
    ```typescript
    const routes: Routes = [
      { path: 'external', loadChildren: () => import('external-lib/module').then(m => m.ExternalModule) },
    ];
    ```  
- **Dynamic Module Federation**: Use Webpack’s Module Federation Plugin for runtime module loading.  
- **NgModules and Components**: Dynamically create components using Angular’s `createComponent`.  

---

### 113. **What Are Signals in Angular 17, and How Do They Differ from Observables and Subjects?**  
- **Definition**: Signals are reactive state primitives introduced in Angular 17 for better reactivity and change detection.  
- **Key Differences**:  
  - Signals are synchronous and more predictable.  
  - Observables support asynchronous streams, while signals focus on state management.  
- **Example**:  
    ```typescript
    const counter = signal(0);
    counter.set(counter() + 1); // Update the signal value
    console.log(counter()); // Read the signal value
    ```  

---

### 114. **How Do Writable Signals Work in Angular, and What Advantages Do They Bring Over BehaviorSubjects or NgRx?**  
- **Writable Signals**: Provide direct methods for reading, setting, and updating state.  
  - Example:  
    ```typescript
    const state = signal({ count: 0 });
    state.update(s => ({ ...s, count: s.count + 1 }));
    ```  
- **Advantages**:  
  - Easier syntax compared to `BehaviorSubject` or `NgRx`.  
  - Built-in integration with Angular’s reactivity system.  

---

### 115. **What Is Angular’s Plan Regarding Signals and Change Detection, and How Will It Impact Performance in Large Applications?**  
- **Plan**: Angular aims to integrate signals fully into its framework for optimized change detection.  
- **Impact on Performance**:  
  - Reduces unnecessary DOM updates.  
  - Works seamlessly with OnPush strategy for better efficiency.  
  - Fine-grained reactivity allows targeting updates to specific components.  

---

### 116. **How Does Angular 17’s Signal System Integrate with Existing State Management Solutions Like NgRx or Services?**  
- **Integration with Services**: Signals can be used in Angular services to manage state instead of `BehaviorSubject` or `ReplaySubject`.  
  - Example:  
    ```typescript
    @Injectable({ providedIn: 'root' })
    export class CounterService {
      count = signal(0);
      
      increment() {
        this.count.set(this.count() + 1);
      }
    }
    ```  
- **Usage with NgRx**: Signals can complement NgRx by simplifying local component state management while using NgRx for global state.  
  - Example: Combine `signal()` for local state and `store.select()` for global state.  
- **Reactive Bindings**: Signals automatically integrate with Angular’s change detection, allowing efficient updates without manual subscriptions.  
- **Backward Compatibility**: Angular ensures signals work alongside existing RxJS-based patterns for a smooth migration.  

--- 