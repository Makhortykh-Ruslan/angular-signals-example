# 🧠 Angular Signals Cheat Sheet (17+)

This README contains all the main Signal APIs that appeared in Angular 17 and newer versions. They replace the classic `@Input`, `@ViewChild`, `@Output`, `ngModel` and other imperative approaches.

## 📦 Requirements

- Angular **17.0** or newer  
- Standalone components  
- Signal-based thinking 🧘

---

## 🔹 input()

> ✅ Replacement for `@Input()`  
> 📦 Available since Angular **17.0**

```ts
import { input } from '@angular/core';

export class ChildComponent {
  name = input<string>();
}
```

```html
<child [name]="someSignal()" />
```

## 🔹 output()

> ✅ Replacement for `@Output()`  
> 📦 Available since Angular **17.0**

```ts
import { output } from '@angular/core';

export class ChildComponent {
  submit = output<void>();
}
```

```html
<child (submit)="onSubmit()" />
```

## 🔹 model()

> ✅ Replacement for `[(ngModel)]`  
> 📦 Available since Angular **17.1**

```ts
import { model } from '@angular/core';

export class CheckboxComponent {
  checked = model<boolean>();
}
```

```html
<checkbox [(checked)]="checkedSignal()" />
```

## Signal queries

## 🔹 viewChild()

> ✅ Replacement for `@ViewChild`  
> 📦 Available since Angular **17.0**

```ts
import { viewChild } from '@angular/core';
import { SomeComponent } from './some.component';

export class ParentComponent {
  child = viewChild(SomeComponent);
  
  constructor() {
    effect(() => {
      console.log(this.child());
    });
  }
}
```

## 🔹 viewChildren()

> ✅ Replacement for `@ViewChildren`  
> 📦 Available since Angular **17.0**

```ts
import { viewChildren } from '@angular/core';
import { SomeComponent } from './some.component';

export class ParentComponent {
  children = viewChildren(SomeComponent);
  
  constructor() {
    effect(() => {
      console.log(this.children());
    });
  }
}
```

## 🔹 contentChild()

> ✅ Replacement for `@ContentChild`  
> 📦 Available since Angular **17.2**

```ts
import { contentChild } from '@angular/core';

export class ParentComponent {
  projected = contentChild(TemplateRef);
  
  constructor() {
    effect(() => {
      console.log(this.projected());
    });
  }
}
```

## 🔹 contentChildren()

> ✅ Replacement for `@ContentChildren`  
> 📦 Available since Angular **17.2**

```ts
import { contentChildren } from '@angular/core';

export class ParentComponent {
  projectedList = contentChildren(TemplateRef);
  
  constructor() {
    effect(() => {
      console.log(this.projectedList());
    });
  }
}
```

## 🔹 afterEveryRender()

> ✅ Replacement for `ngAfterViewChecked()`  
> 📦 Available since Angular **17.2**

```ts
import { afterEveryRender, viewChild } from '@angular/core';
import { MyComponent } from './my.component';

export class AppComponent {
  comp = viewChild(MyComponent);
  
  constructor() {
    afterEveryRender(() => {
      console.log('Rendered:', this.comp());
    });
  }
}
```

## 🔹 afterNextRender()

> ✅ Replacement for `ngAfterViewInit()`  
> 📦 Available since Angular **17.2**

```ts
import { afterNextRender } from '@angular/core';

afterNextRender(() => {
  console.log('First render complete!');
});
```

## 🔹 effect()

> ✅ Reactive lifecycle hook  
> 📦 Available since Angular **16.0**

```ts
import { effect, signal } from '@angular/core';

const count = signal(0);

effect(() => {
  console.log('Count changed:', count());
});
```

## Comparison Table

| Classic API              | Signal API           | Angular |
| ------------------------ | -------------------- | ------- |
| `@Input()`               | `input()`            | 17.0    |
| `@Output()`              | `output()`           | 17.0    |
| `[(ngModel)]`            | `model()`            | 17.1    |
| `@ViewChild`             | `viewChild()`        | 17.0    |
| `@ViewChildren`          | `viewChildren()`     | 17.0    |
| `@ContentChild`          | `contentChild()`     | 17.2    |
| `@ContentChildren`       | `contentChildren()`  | 17.2    |
| `ngAfterViewInit()`      | `afterNextRender()`  | 17.2    |
| `ngAfterViewChecked()`   | `afterEveryRender()` | 17.2    |
| `ngOnInit`/`ngOnChanges` | `effect()`           | 16.0    |
