---
layout: post
title: "Using Renderer2 Inside Services in Angular"
date: 2017-12-15 14:13:00 +0200
---

Since Angular 4 was released `Renderer` class becomes `@deprecated` and replaced by `Renderer2`. It's very frustrating to have Renderer2 as a name of class in world famous framework. That means when Renderer will be deleted in Angular version 5 or 6 from framework only Renderer2 will stay to exist. Without any connection with reality, producing hundred of questions "Why it calls Renderer2 and there is Renderer1?". Anyway it's a good topic for different post of criticism around Angular2 (4, 5, any).

### First I will share the solution:

```typescript
import { Renderer2, RendererFactory2 } from '@angular/core';

@Injectable()
class Service {
    private renderer: Renderer2;
    
    constructor(rendererFactory: RendererFactory2) {
        this.renderer = rendererFactory.createRenderer(null, null);
    }
}
```
---
*Steps of problem solving then you faced with the problem.*

### It's not a good idea to inject Renderer2 in Service.

By design services should request and process data and control workers. The quote from Angular official docs on Services pages:

Components shouldn't fetch or save data directly and they certainly shouldn't knowingly present fake data. They should focus on presenting data and delegate data access to a service."

That's it. Only data, without any event tracking, DOM or Renderer access. So first if you want to use `Renderer2` inside a service, try to find soluton using Directive or Component for Renderer injection.

### Unhandled Promise rejection: StaticInjectorError[Renderer2]

Congrats! You finally decided to break the rules and inject Renderer2 in your Service. More likely your code looks like the following:

```typescript
import { Renderer2 } from '@angular/core';

@Injectable()
class Service {
  constructor(private renderer: Renderer2) {
  }
}
```

Then injecting Renderer2 to Service you will get an Error (presented below) because Renderer can be injected only to Component or Directive.
The error:

```
Unhandled Promise rejection: StaticInjectorError[Renderer2]: 
  StaticInjectorError[Renderer2]: 
    NullInjectorError: No provider for Renderer2! ; Zone: <root> ; Task: Promise.then ; Value: Error: StaticInjectorError[Renderer2]: 
  StaticInjectorError[Renderer2]: 
    NullInjectorError: No provider for Renderer2!
```

The first thought is to get Renderer2 from some Component:

```
import { Renderer2 } from '@angular/core';

class Component {
  constructor(service: Service, renderer: Renderer2) {
      service.renderer = renderer;
  }
}

@Injectable()
class Service {
  public renderer: Renderer2;
}
```

And it will solve the problem. Except of your binding to component and hard dependency between the Service and the Component. And also it forces `renderer` attribute to be `public`, which will not make happy your github reviewer who has deep Java experience.


### Discovering RendererFactory2

After you got stacked on problem solving with a framework not telling you how to solve the particular case you should go to the roots, framework sources I mean.

In angular [sources](https://github.com/angular/angular/blob/5.1.1/packages/core/src/render/api.ts#L128) we can discover `RendererFactory2` which can return `Renderer2` instance by using `RendererFactory2.createRenderer` method.

And Angular itself internaly uses RendererFactory2 for the same proposes.

Example:

```typescript
// https://github.com/angular/angular/blob/3ce3b4d2afdc5198a9a5a9432db1f88e2e5d1972/packages/core/src/view/services.ts#L128
const renderer = rendererFactory.createRenderer(null, null);
```

--
Related to:

Angular Issue - [Error: No Provider for Renderer 2!](https://github.com/angular/angular/issues/17824)

Stackoverflow -
- [https://stackoverflow.com/questions/44812394](https://stackoverflow.com/questions/44812394/error-no-provider-for-renderer2-angular-v-4-1-3)
- [https://stackoverflow.com/questions/43070308](https://stackoverflow.com/questions/43070308/using-renderer-in-angular-4)
- [https://stackoverflow.com/questions/44989666](https://stackoverflow.com/questions/44989666/angular-4-service-no-provider-for-renderer2)
- [https://stackoverflow.com/questions/47644070/how-to-inject-renderer2-into-custom-service-in-angular-4](https://stackoverflow.com/questions/47644070/how-to-inject-renderer2-into-custom-service-in-angular-4)
