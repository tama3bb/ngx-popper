# ngx-popper  

[![npm](https://img.shields.io/npm/v/ngx-popper.svg?style=flat-square)](https://www.npmjs.com/package/ngx-popper) 
[![npm](https://img.shields.io/npm/dm/ngx-popper.svg?style=flat-square)](https://www.npmjs.com/package/ngx-popper) 
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](https://github.com/MrFrankel/ngx-popper/blob/master/LICENSE)
  <img src="http://badge-size.now.sh/https://unpkg.com/ngx-popper@2.0.1/ngx-popper.js?compression=brotli" alt="Stable Release Size"/>
  <img src="http://badge-size.now.sh/https://unpkg.com/ngx-popper@2.0.1/ngx-popper.js?compression=gzip" alt="Stable Release Size"/>

ngx-popper is an angular wrapper for the [Popper.js](https://popper.js.org/) library.

### Installation

node and npm are required to run this package.

1. Use npm/yarn to install the package:

  ```terminal
  $ npm install ngx-popper --save 
  ```
  
  Or 
  
   ```terminal
    $ yarn add ngx-popper --save 
  ```

2. You simply add into your module `NgxPopperModule`:

  ```typescript
  import {NgxPopperModule} from 'ngx-popper';
  
  @NgModule({
   // ...
   imports: [
     // ...
     NgxPopperModule
   ]
  })
  ```
  
SystemJS 
```
    System.config({
        paths: {
            // paths serve as alias
            'npm:': 'libs/'
        },
        // map tells the System loader where to look for things
        map: {
            ... ,
            'ngx-popper': 'npm:ngx-popper',
            'popper-directive.js': 'npm:ngx-popper',
            'popper.module': 'npm:ngx-popper',
        },
        // packages tells the System loader how to load when no filename and/or no extension
        packages: {
            ... ,
            'ngx-popper': {
                main: 'index.js',
                defaultExtension: 'js'
            },
            'popper.js': {
                main: 'popper-directive.js',
                defaultExtension: 'js'
            },
            'popper.module': {
                main: './popper.module.js',
                defaultExtension: 'js'
            }
        }
    });

```
  

3. Add to view:

  ```HTML  
   <div     [popper]="popper1Content"
            [popperShowOnStart]="true"
            [popperTrigger]="'click'"
            [popperPlacement]="'bottom'">
         <p class="bold">Hey!</p>
         <p class="thin">Choose where to put your popper!</p>         
       </div>
       <popper-content #popper1Content>
         <p class="bold">Popper on bottom</p>
       </popper-content>
  ```

4. As text:
 ```HTML
      <div [popper]="'As text'"
           [popperTrigger]="'hover'"
           [popperPlacement]="'bottom'"
           (popperOnShown)="onShown($event)">
        <p class="bold">Pop</p>
        <p class="thin">on the bottom</p>
      </div>
 ```

  ```HTML
       <div popper="{{someTextProperty}}"
            [popperTrigger]="'hover'"
            [popperPlacement]="'bottom'"
            (popperOnShown)="onShown($event)">
         <p class="bold">Pop</p>
         <p class="thin">on the bottom</p>
       </div>
  ```
 
  5. Position fixed, breaking overflow:
   ```HTML
        <div [popper]="'As text'"
             [popperTrigger]="'hover'"
             [popperPlacement]="'bottom'"
             [popperPositionFixed]="true"
             (popperOnShown)="onShown($event)">
        </div>
   ```
 
 6. Specific target:
  ```HTML
 <div class="example">
       <div #popperTargetElement></div>
       <div [popper]="'As text'"
            [popperTrigger]="'hover'"
            [popperPlacement]="'bottom'"
            [popperTarget]="popperTargetElement"
            (popperOnShown)="onShown($event)">
       </div>
  ```
  
7. hide/show programmatically:
  ```HTML
   <div [popper]="tooltipcontent"
           [popperTrigger]="'hover'"
           [popperPlacement]="'bottom'">
           [popperApplyClass]="'popperSpecialStyle'"
        <p class="bold">Pop</p>
        <p class="thin">on the bottom</p>
      </div>
      <popper-content #tooltipcontent>
        <div>
          <p>This is a tooltip with text</p>
          <span (click)="tooltipcontent.hide()">Close</div>
        </div>
      </popper-content>
  ```
 
8. Attributes map:  
  
    | Option                   | Type              | Default   | Description                                                                                              |
    |:-------------------      |:----------------  |:--------- | :------------------------------------------------------------------------------------------------------  |
    | popperDisableAnimation   | boolean           | false     | Disable the default animation on show/hide                                                               |
    | popperDisableStyle       | boolean           | false     | Disable the default styling                                                                              |
    | popperDisabled           | boolean           | false     | Disable the popper, ignore all events                                                                    |
    | popperDelay              | number            | 0         | Delay time until popper it shown                                                                         |
    | popperTimeout            | number            | 0         | Set delay before the popper is hidden                                                                    |
    | popperTimeoutAfterShow   | number            | 0         | Set a time on which the popper will be hidden after it is shown                                          |
    | popperPlacement          | Placement(string) | auto      | The placement to show the popper relative to the reference element                                       |
    | popperTarget             | HtmlElement       | auto      | Specify a different reference element other the the one hosting the directive                            |
    | popperBoundaries         | string(selector)  | undefined | Specify a selector to serve as the boundaries of the element                                             |
    | popperShowOnStart        | boolean           | false     | Popper default to show                                                                                   |
    | popperTrigger            | Trigger(string)   | hover     | Trigger/Event on which to show/hide the popper                                                           |
    | popperPositionFixed      | boolean           | false     | Set the popper element to use position: fixed                                                            |
    | popperHideOnClickOutside | boolean           | true      | Popper will hide on a click outside                                                                      |
    | popperHideOnScroll       | boolean           | false     | Popper will hide on scroll                                                                               |
    | popperHideOnMouseLeave   | boolean           | false     | Popper will hide on mouse leave                                                                          |
    | popperForceDetection     | boolean           | false     | Force the popper to trigger detection event, in case the parent component use onPush strategy            |
    | popperModifiers          | popperModifier    | undefined | popper.js custom modifiers hock                                                                          |
    | popperApplyClass         | string            | undefined | list of comma separated class to apply on ngpx__container                                                |
    | popperApplyArrowClass    | string            | undefined | list of comma separated class to apply on ngpx__arrow                                                    |
    | popperOnShown            | EventEmitter<void>| $event    | Event handler when popper is shown                                                                       |
    | popperOnHidden           | EventEmitter<void>| $event    | Event handler when popper is hidden                                                                      |
    | popperAriaDescribeBy     | string            | undefined | Define value for aria-describeby attribute                                                               |
    | popperAriaRole           | string            | popper    | Define value for aria-role attribute                                                                     |



9. Override defaults:

    Ngx-popper comes with a few default properties you can override in default to effect all instances
    These are overridden by any child attributes.
```JavaScript
NgModule({
  imports: [
    BrowserModule,
    FormsModule,
    NgxPopperModule.forRoot({placement: 'bottom'})],
  declarations: [AppComponent],
  providers: [],
  bootstrap: [AppComponent]

})
```
  
   | Options                  | Type              | Default   |
   |:-------------------      |:----------------  |:--------- |
   | showDelay                | number            | 0         |
   | disableAnimation         | boolean           | false     |
   | disableDefaultStyling    | boolean           | false     |
   | placement                | Placement(string) | auto      |
   | boundariesElement        | string(selector)  | undefined |
   | trigger                  | Trigger(string)   | hover     |
   | popperModifiers          | popperModifier    | undefined |
   | positionFixed            | boolean           | false     |
   | hideOnClickOutside       | boolean           | true      |
   | hideOnMouseLeave         | boolean           | false     |
   | hideOnScroll             | boolean           | false     |
   | applyClass               | string            | undefined |
   | applyArrowClass          | string            | undefined |
   | ariaDescribeBy           | string            | undefined |
   | ariaRole                 | string            | undefined |

10. popperPlacement:

  | 'top'
  | 'bottom'
  | 'left'
  | 'right'
  | 'top-start'
  | 'bottom-start'
  | 'left-start'
  | 'right-start'
  | 'top-end'
  | 'bottom-end'
  | 'left-end'
  | 'right-end'
  | 'auto'
  | 'auto-top'
  | 'auto-bottom'
  | 'auto-left'
  | 'auto-right'
  | Function
  
11. popperTrigger:

  | 'click'
  | 'mousedown'
  | 'hover'
  | 'none'
  
    
### Demo
<a href="https://mrfrankel.github.io/ngx-popper/">Demo</a>

### Contribute
  Hell ya!!!
  
```terminal
  $ yarn install
  $ yarn run build
  $ yarn run dev  
```

