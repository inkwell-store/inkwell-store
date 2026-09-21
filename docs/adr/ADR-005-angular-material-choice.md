# Angular material choice

## Context
A good User Experience (UX) involves the implementation of visual components that are consistent, intuitive and responsive. At the same time Graphical User Interfaces (GUI) are notoriously hard to build and for web development many tools were released to help developers build these GUI.

In the universe of Angular there are a few options available, which with their own strengths.

## Options considered
1. Bootstrap (via NgBootstrap)
2. Angular Materials
3. PrimeNg
4. Build my own components using pure css, scss and sass
5. Build my own components Tailwindd
6. Combine a component framework, like PrimeNg, Angular materials or NgBootstrap with tailwind.

## Decision
Choosing **option 6** seems the better choice, and I chose Angular Materials with Tailwind. The reason for tailwind is because of its powerful classes system, especially when it comes to responsive desing. I can easily create reponsive UI components using css classes most importantly, make them consistent and predictable. Unfortunately tailwind classes sometimes don't work well with angular components. Imagine the following example:

```html
<my-ng-component class="bg-red-700 text-center"></my-ng-component>
```

Because of how angular components are created this tailwind class might not apply to the angular component. This is something that **can** in material's components **sometimes**. Even with this, tailwind is a fantatistc tool still worth it to use this case.

Angular material is a better choice when compared to others because it's maintained by the Angular's team at google. This means the components implemented by the library are integrated with angular by design. Also, the Material Design from google offers a consistent layout and style for components, integrated well with google fonts, material icons and material themes. 

## Consequences
* Although a UI library can be customizable it can be difficult to avoid maintain consistency when designing my own components.
* Once a UI library is choosen it can lock you out of other options, either due to compatibility or visual appearence.
* Iteration becomes dramatically faster and easier because of material's components.
* Using a UI library can make your website very similar to others, precisely because the styles are the same.