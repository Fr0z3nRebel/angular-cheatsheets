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