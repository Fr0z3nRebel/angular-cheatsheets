# Lifecycle Hooks

Lifecycle hooks are special methods that Angular calls at different stages of a component or directive's lifecycle. They allow you to perform custom logic at specific points in time, such as when a component is initialized, when its inputs change, or when it is destroyed.

## Contents
1. [Order of Execution](#order-of-execution)
2. [Example Usage](#example-usage)
3. [Tips for Using Lifecycle Hooks](#tips-for-using-lifecycle-hooks)
4. [Additional Notes](#additional-notes)
    1. [ngOnChanges](#ngonchanges)
    2. [ngOnInit](#ngoninit)
    3. [ngDoCheck](#ngdocheck)


## Order of Execution

| Hook                    | Purpose |
| ---                     | --- |  
| `ngOnChanges`           | Called when any data-bound property changes |
| `ngOnInit`              | Called once when the component is initialized |
| `ngDoCheck`             | Called during every change detection run |
| `ngAfterContentInit`    | Called after external content is projected |
| `ngAfterContentChecked` | Called each time projected content is checked |
| `ngAfterViewInit`       | Called after a component's view is initialized |
| `ngAfterViewChecked`    | Called after a component's view is checked |
| `ngOnDestroy`           | Called before a component is destroyed |

## Example Usage

```typescript
import {
  Component,
  OnChanges,
  OnInit,
  DoCheck,
  AfterContentInit,
  AfterContentChecked,
  AfterViewInit,
  AfterViewChecked,
  OnDestroy
} from '@angular/core';

@Component(...) 
export class ExampleComponent implements OnChanges, OnInit, DoCheck,  
AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy {

  constructor() {
    // Called first time a component is instantiated
  }

  ngOnChanges() {
    // Called before ngOnInit() and whenever a data-bound input property changes
  }

  ngOnInit() {
    // Called after the component is created and its input properties are updated
    // Called once after the first ngOnChanges()
  }

  ngDoCheck() {
    // Called on every change and immediately after ngOnChanges() and ngOnInit()
  }

  ngAfterContentInit() {
    // Called after ngDoCheck(), when external content is projected into a component
  }

  ngAfterContentChecked() {
    // Called after ngAfterContentInit() and every subsequent ngDoCheck()
  }

  ngAfterViewInit() {
    // Called after ngAfterContentChecked() and after component's view is initialized
  }

  ngAfterViewChecked() {
    // Called after ngAfterViewInit() and every subsequent ngAfterContentChecked()
  }

  ngOnDestroy() {
    // Called immediately before a directive, pipe, or component is destroyed
  }

}
```

## Additional Notes

### ngOnChanges

* Available for components and directives
* Only called when an input property's reference has changed
  * ie. Pushing a value to an array will not trigger `ngOnChanges`

### ngOnInit

* Available for components and directives
* Called only one time, during the very first change detection cycle
* Called after the component is created and its input properties are updated, right after `ngOnChanges` is called
* When called, child components and projected contents are not yet available, because the view has not been created yet
  * ie. `@ViewChild`, `@ViewChildren`, `@ContentChild`, `@ContentChildren`
* Available for components and directives

### ngDoCheck

* Available for components and directives
* Called during every change detection cycle
* Called after `ngOnChanges` and `ngOnInit`
* Called even if there is no change in input bound properties
  * ie. When a button is clicked even if the button doesn't do anything
* Use to implement custom change detection when Angular doesn't detect any changes to input bound properties
* Use when you want to execute some code on every change detection cycle
  * Called very frequently, and can cause performance issues if overused
* When called, child components are available, but projected contents are not yet available

### ngAfterContentInit

* Available for components only: not available for directives
* Called only one time, during the very first change detection cycle
* Called after the projected content has been initialized
* Called even if there is no projected content
* Called after `@ContentChild` and `@ContentChildren` properties have been updated

### ngAfterContentChecked

* Available for components only: not available for directives
* Called during every change detection cycle
* Called after the projected content has been initialized, checked, and updated
* Called even if there is no projected content
* Called even if no projected content has changed
* Called after `@ContentChild` and `@ContentChildren` properties have been updated

### ngAfterViewInit

* Available for components only: not available for directives
* Called only one time, during the very first change detection cycle
* Called after the view template and all descendant child components' view templates are initialized
* Called after `@ViewChild` and `@ViewChildren` properties have been updated
* When called, all lifecycle hooks and directives of all descendant child components are already called, and all descendant child components are completely ready

### ngAfterViewChecked

* Available for components only: not available for directives
* Called during every change detection cycle
* Called after the view template and all descendant child components' view templates are checked and updated
* Called after `@ViewChild` and `@ViewChildren` properties have been updated

### ngOnDestroy

* Available for components and directives
* Called just before the component or directive is destroyed (removed from the DOM)
* Great place to implement any cleanup work
  * ie. Unsubscribe from an observable, detach event handler, etc.

## ~~Tips for Using Lifecycle Hooks~~

* Use `ngOnInit` to initialize the component and perform any one-time setup tasks.
* Use `ngOnChanges` to respond to changes in input properties.
* Use `ngDoCheck` to perform custom change detection.
* Use `ngAfterContentInit` and `ngAfterContentChecked` to respond to changes in projected content.
* Use `ngAfterViewInit` and `ngAfterViewChecked` to respond to changes in the component's view.
* Use `ngOnDestroy` to clean up resources before the component is destroyed.
