## How does Angular know that the value of a property has changed?
Angular runs a Change Detection Cycle on every event that happens on the DOM.
- When a component's `@input` property has changed
- When a DOM event happens (ie. `click` or `change`)
- When a timer event happens (ie. `setTimeout()` or `setInterval()`)
- When an HTTP request is made

## When does a component's @Input property get populated and become available?
- When the component's constructor is called, its `@Input` properties are not immediately available.
- The child components are not constructed
- Projected contents are not available on that component yet
 - This all happens when the constructor execution is complete
 - Once instantiated, Angular lifecycle beings

 ## Directives

 ### Component Directive
 The component directive is simply a component. It is a directive with a template.

 ### Attribute Directive
 The attribute directive changes the appearance or behavior of a DOM element.

 ### Structural Directive
 The structural directive adds or removes a DOM element.

 ## DOM Manipulation

 1. Angular keeps the component and view in sync using templates, change detection, data binding, etc. All of those are bypassed if you update the DOM directly.

 2. DOM manipulation only works in browsers. You can't manipulate the DOM directly on other platforms like desktop or mobile apps, web workers, or servers for server-side rendering, etc. where there is no browser.

 3. DOM APIs do not sanitize any data. This is a security vulnerability and makes it possible for a malicious actor to inject scripts and carry out what are known as XSS injection attacks.

 ### Renderer 2

- Allows us to manipulate the DOM without accessing the DOM elements directly
- Provides a layer of abstraction between the DOM element and the component code

 ```TypeScript
constructor(private element: ElementRef, private renderer: Renderer2) {}

ngOnInit() {
  this.renderer.setStyle(this.element.nativeElement, 'backgroundColor', '#36454F');
  this.renderer.setStyle(this.element.nativeElement, 'color', 'yellow');
}
 ```

### @HostListener

- Listens to a DOM event on the host element and executes an event handler method in response to that event.

```TypeScript
@HostListener('mouseenter') OnMouseEnter() {
  // Do something
}
```