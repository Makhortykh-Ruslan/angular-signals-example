# 🧠 Angular Signals Cheat Sheet (17+)

Цей README містить усі основні Signal API, які зʼявились в Angular 17 і новіших версіях. Вони приходять на заміну класичним `@Input`, `@ViewChild`, `@Output`, `ngModel` та іншим імперативним підходам.

## 📦 Вимоги

- Angular **17.0** або новіше  
- Standalone компоненти  
- Signal-based thinking 🧘

---

## 🔹 input()

> ✅ Заміна `@Input()`  
> 📦 Зʼявилось в Angular **17.0**

```ts
import { input } from '@angular/core';

export class ChildComponent {
  name = input<string>();
}

<child [name]="someSignal()" />
```

## 🔹 output()

> ✅ Заміна `@Output()`
> 📦 Зʼявилось в Angular **17.0**

```ts
import { output } from '@angular/core';

export class ChildComponent {
  submit = output<void>();
}

<child (submit)="onSubmit()" />

```


## 🔹 model()

> ✅ Заміна `[(ngModel)]`
> 📦 Зʼявилось в Angular **17.1**

```ts
import { model } from '@angular/core';

export class CheckboxComponent {
  checked = model<boolean>();
}

<checkbox [(checked)]="checkedSignal()" />

```


## 🔹 model()

> ✅ Заміна `[(ngModel)]`
> 📦 Зʼявилось в Angular **17.1**

```ts
import { model } from '@angular/core';

export class CheckboxComponent {
  checked = model<boolean>();
}

<checkbox [(checked)]="checkedSignal()" />

```


## Signal queries

## 🔹 viewChild()

> ✅ Заміна `@ViewChild`
> 📦 Зʼявилось в Angular **17.0**

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

> ✅ Заміна `@ViewChildren`
> 📦 Зʼявилось в Angular **17.0**

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

> ✅ Заміна `@ContentChild`
> 📦 Зʼявилось в Angular **17.2**

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

> ✅ Заміна `@ContentChildren`
> 📦 Зʼявилось в Angular **17.2**

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

> ✅ Заміна `ngAfterViewChecked()`
> 📦 Зʼявилось в Angular **17.2**

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

> ✅ Заміна `ngAfterViewInit()`
> 📦 Зʼявилось в Angular **17.2**

```ts
import { afterNextRender } from '@angular/core';

afterNextRender(() => {
  console.log('First render complete!');
});

```

## 🔹 effect()

> ✅ Реактивний lifecycle hook
> 📦 Зʼявилось в Angular **16.0**

```ts
import { effect, signal } from '@angular/core';

const count = signal(0);

effect(() => {
  console.log('Count changed:', count());
});


```




| Класичний API            | Signal API           | Angular |
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

