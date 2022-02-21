# Angular

* [Definition](#definition)
    * [Advantages](#advantages)
    * [Disavantages](#disavantages)
* [Lifecycle](#Lifecycle)
* [Interceptors](#interceptors)
* [Zones](#zones)
    * [NgZone](#ngzone)
    * [OutsideZone](#outsidezone)
* [Change Detection Strategy](#change-detection-strategy)
    * [Default Change Detection Strategy](#default-change-detection-strategy)
    * [onPush Change Detection Strategy](#onpush-change-detection-strategy)
* [AOT and JIT Compiler](#aot-and-jit-compiler)
    * [AOT](#aot)
    * [JIT](#jit)

## Definition
- Angular is an application design framework and development platform for creating efficient and sophisticated single-page apps.

## Advantages
- First-class Typescript support.
- Benefits of ES6 and new versions.
- Super powerful CLI.
- Dependency Injection
- Modular, cross platform.
- All in Solution (including routing, forms management, client-server communication, and more)

## Disavantages
- A lot to learn for beginners, framework, Typescript, and RxJs.
- Bundle size.
- Community size.

# Lifecycle
- `constructor`
- `ngOnChanges()`
- `ngOnInit()` 
- `ngDoCheck()`
- `ngAfterContentInit()`
- `ngAfterContentChecked()`
- `ngAfterViewInit()`
- `ngAfterViewChecked()`
- `ngOnDestroy()`

# Interceptors
- Interceptors are a unique type of Angular Service that we can implement. Interceptors allow us to intercept incoming or outgoing HTTP requests using the HttpClient. By intercepting the HTTP request, we can modify or change the value of the request.
  - Handling HTTP Headers
  - HTTP Response Formatting
  - HTTP Error Handling

```js 
@Injectable()
export class MyInterceptor implements HttpInterceptor {
  intercept(httpRequest: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    return next.handle(httpRequest);
  }
}

@NgModule({
  imports: [BrowserModule, HttpClientModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent],
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: MyInterceptor, multi: true }
  ]
})
export class AppModule { }
```

# Zones
- Are a sort of execution context that allows us to hook into our asynchronous tasks.
- It turns out that, the problem that Zones solve, plays very nicely with what Angular needs in order to perform change detection in our applications
- Application state change is caused by three things:
 - Events - User events like click, change, input, submit, …
 - XMLHttpRequests - E.g. when fetching data from a remote service
 - Timers - setTimeout(), setInterval(), because JavaScript

## NgZone
- NgZone is basically a forked zone that extends its API and adds some additional functionality to its execution context.

- ChangeDetect runs every time `onTurnDone()` is called.

  - `onTurnStart()` - Notifies subscribers just before Angular’s event turn starts. Emits an event once per browser task that is handled by Angular.
  - `onTurnDone()` - Notifies subscribers immediately after Angular’s zone is done processing the current turn and any micro tasks scheduled from that turn.
  - `onEventDone()` - Notifies subscribers immediately after the final onTurnDone() callback before ending VM event. Useful for testing to validate application state.

## OutsideZone
```js
processOutsideAngularZone() {
  this.progress = 0;
  this.zone.runOutsideAngular(() => {
    this.increaseProgress(() => {
      this.zone.run(() => {
        console.log('Outside Done!');
      });
    });
  });
}
```

- https://blog.thoughtram.io/angular/2016/02/01/zones-in-angular-2.html

# Change Detection Strategy
- Angular Change Detection Strategy are the methods by which the updates to the component is tracked and component is triggered to Re-render

## Default Change Detection Strategy
- Change detection cycle runs of each and every event that occur inside the Component.
- Click Event of Elements, Receiving Data via Asynchronous Call, Triggering setTimeout and setInterval

- [Cons] Every time a parent component gots re-rendered, the ChildComponent life Cycle is also triggered to re-render even if no inputs/outputs between both.

## onPush Change Detection Strategy
- The ChildComponent is not always dirty checked, if the parent element is updating the values that are not passed as “@Input” properties to the Child Component, then the child Component should not be dirty checked.

- [Pros] No Unnecessary Dirty Check in the Child Components
- [Pros] Faster Component Re-rendering
- [Pros] Listen for changes on @Input() and pipe `async` on the template

- [Cons] Works only for immutable objects, since Angular looks for a change on the reference in the @Input()
- [Cons] For specific scenarios, need to run `componentRef.markForCheck()`

# AOT and JIT Compiler

## AOT
- It's a process of compiling higher-level language or intermediate language into a native machine code. When you serve/build your angular application, the Ahead of Time compiler converts your code during the build time before your browser downloads and runs that code.

- [Pros] Loading in AOT is much quicker than the JIT because it already has compiled your code at build time.
- [Pros] AOT is much suitable in the case of Production mode.
- [Pros] AOT provides a big benefit to angular developers for production mode by reducing bundle size and making your app render faster
## JIT
- Just in time compiler provides compilation during the execution of the program at a run time before execution. In simple words, code get compiles when it’s needed, not at the build time.

- [Pros] Most compiling is done on the browser side, so it will take less compiling time.
- [Pros] JIT is more suitable for development mode.
- [Pros] Implementing features and debugging is easy in JIT mode since you have to map files.