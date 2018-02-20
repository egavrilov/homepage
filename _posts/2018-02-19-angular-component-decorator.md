---
ID: 37
post_title: Angular @Component Decorator
author: huncode
post_excerpt: ""
layout: post
permalink: >
  https://huncode.com/angular-component-decorator/
published: true
post_date: 2018-02-19 14:41:46
---
## All you might know about @Component Angular Decorator
TypeScript has a nice feature called Decorators. Also, they are proposed to be a part of JavaScript and you can found current status on the project GitHub page. [^1]

Decorators can be attached to class, method, property, parameter or accessor.
Decorators use the format `@expression`, where `expression` must be a function that will be called at runtime with information about the decorated declaration.

```typescript
/**
 * This is an example of all possible variants using Decorators in TypeScript
 * All the cases of use has explanation section below
 */

@component                 // component decorator on class declaration
class Component {
  @defaultValue x = 12     // defaultValue decorator on property

  @first                   // first and second decorator on private method, 
  @second                  // can be also written on one line as
  private create() { ... } // @first @second private create() { ... }

  @modifier(false)         // decorator can return function to call
  set tenfold (value) {    // decorator on accessor
    this.x = value * 10;
  }

  constructor(@only param) {} // decorator @only on function param
}

// Decorators must evaluate to a function

function component(constructor: Function) {
 // ... process Component class construction function or even replace it
}

function first () { ... }

// TODO: add all cases of usage... or not (vote in comments!)

```

#### Angular @Component decorator
@Component decorator with all possible params set:

Short:

Metadata Properties:
- animations - list of animations of this component
- changeDetection - change detection strategy used by this component
- encapsulation - style encapsulation strategy used by this component
- entryComponents - list of components that are dynamically inserted into the view of this component
- exportAs - name under which the component instance is exported in a template
- host - map of class property to host element bindings for events, properties and attributes
- inputs - list of class property names to data-bind as component inputs
- interpolation - custom interpolation markers used in this component's template
- moduleId - ES/CommonJS module id of the file in which this component is defined
- outputs - list of class property names that expose output events that others can subscribe to
- providers - list of providers available to this component and its children
- queries - configure queries that can be injected into the component
- selector - css selector that identifies this component in a template
- styleUrls - list of urls to stylesheets to be applied to this component's view
- styles - inline-defined styles to be applied to this component's view
- template - inline-defined template for the view
- templateUrl - url to an external file containing a template for the view
- viewProviders - list of providers available to this component and its view children

Long:

```typescript
import { animate, style, transition } from &#039;@angular/animations&#039;;
import { ChangeDetectionStrategy, Component, ViewEncapsulation } from &#039;@angular/core&#039;;

@Component({
```
---
  **changeDetection:** Defined detection strategy to use in component. It means that change detectors mode will be initially set to
  - `CheckOnce` (`ChangeDetectionStrategy.OnPush` Strategy)
  - `CheckAlways`(`ChangeDetectionStrategy.Default` Strategy)

```typescript
  changeDetection: ChangeDetectionStrategy.OnPush,
```
---
  **viewProviders:** Defines the set of injectable objects that are visible to its view DOM children.
  Allows you to prevent projected content children (`<ng-content>...</ng-content>`) from accessing listed services.

```typescript
  viewProviders: [OnlyCurrentComponentAvailableService],
```
---
  **providers:** `OnlyCurrentComponentAvailableService` couldn't be injected into projected content.
  So `viewProviders` limits the provider to children other than projected content, while `providers` allows all children to use the provider.

  Defines the set of injectable objects that are visible to a Component and its light DOM children.
  Access to `AnyChildAccessableService` is available for all children.

```typescript
  providers: [AnyChildAccessableService],
```
---
  **moduleId:** The module id of the module that contains the component. Needed to be able to resolve relative urls for templates and styles. Value should be set depends on you module build:

  If you use :
  - `Webpack` - you don't need to set any value
  - `CommonJS` - make sure value is `module.id`
  - `SystemJS` - make sure value is `__moduleName`

```typescript
  moduleId: module.id,
```
---
  **templateUrl:, template:** Relative Url to Component template or inline template for an Angular Component. Only one of `templateUrl` or `template` can be defined per Component.

```typescript
  templateUrl: &#039;my.component.html&#039;,
  template: &#039;&lt;div&gt;MyComponent exist and works well!&lt;div&gt;&#039;,
```
---
  **styleUrls:, styles:** Specifies stylesheet URLs for an Angular component.
  If you use `@angular/cli`, you can use preprocessors (LESS, SASS, SCSS, Stylus) or even mix preprocessor languages if you really need.

```typescript
  styleUrls: [&#039;../common-style.scss&#039;, &#039;my.component.css&#039;],
  styles: &#039;div { color: cadetblue; }&#039;,
```
---
  **animations:**  Special <abbr title="Domain Specific Language">DSL</abbr> to desscribe animations by listening on state changes.

  Transition values might be `:enter`, `:leave`, `* => *`, `* => stateName`, `oldState => newState`.
  I like [^this guide](https://www.yearofmoo.com/2017/06/new-wave-of-animation-features.html) about Angular animations.

```typescript
  animations: [
    transition(&#039;:enter&#039;, [
      style({transform: &#039;translateX(-100%)&#039;}),
      animate(100)
    ]),
    transition(&#039;:leave&#039;, [
      animate(100, style({transform: &#039;translateX(100%)&#039;}))
    ])
  ],
```
---
  **encapsulation:** Specify encapsulation of styles and template of the component.
  Default value is taken from `CompilerOptions`, currently it is `ViewEncapsulation.Emulated`.

  Possible values of `enum ViewEncapsulation` are:
  - `ViewEncapsulation.Emulated` - Emulate `Native` scoping of styles by adding an attribute containing surrogate id to the Host Element and pre-processing the style rules provided via styles or styleUrls, and adding the new Host Element attribute to all selectors.
  - `ViewEncapsulation.Native` - Use the native encapsulation mechanism of the renderer. Current browsers support: [link](https://caniuse.com/#feat=shadowdom)
  - `ViewEncapsulation.None`- Don't provide any template or style encapsulation.

```typescript
  encapsulation: ViewEncapsulation.Native,
```
---
  **interpolation:**
  Overrides the default encapsulation start and end delimiters. Default value is `['{{', '}}']`

```typescript  
  interpolation: [&#039;{&#039;, &#039;}&#039;], // React style single brace delimiters
```
---
  entryComponents: Array<Type<any> | any[]>
  preserveWhitespaces: boolean
  // inherited from core/Directive
  selector: string
  inputs: string[]
  outputs: string[]
  host: {...}
  exportAs: string
  queries: {...}
})
export class NameComponent {
  constructor() { }

  ngOnInit() { }
}
```
### Performance of decorators

Decorators evaluate in runtime

[^1]: Decorators proposal <a href="https://github.com/tc39/proposal-decorators">GitHub page</a>
[^2]: Angular Official <a href="https://angular.io/guide/cheatsheet">Cheatsheet</a>