# Angular Major Updates

* [v12](#v12)
* [v13](#v13)
* [v14](#v14)
* [v15](#v15)
* [v16](#v16)
* [v17](#v17)

# v12
- Support for TypeScript 4.2
- Support for Webpack 5
- Stylish Improvements (support inline sass on component declaration)
- Nullish Coalescing in templates (??)

# v13
- Support for TypeScript 4.4
- Support for RxJS 7.4
- Enhancements to Angular Tests (performance)
- Deprecated Support for IE11
- 100% Ivy and No More Support for View Engine (all internal tools use Ivy now)

# v14
- Standalone components, directives and pipes
- Typed angular forms (ensures that values are type-safe)
- Bind protected members now works


```js
@Component({
  standalone: true,
  selector: 'photo-gallery',
  imports: [ImageGridComponent],
  template: `
    ... <image-grid [images]="imageList"></image-grid>
  `,
})
export class PhotoGalleryComponent {}
```

```js
export class SampleComponent {
   contactForm = new FormGroup({
     name: new FormControl<string>('', { nonNullable: true }),
     email: new FormControl<string>('', { nonNullable: true }),
     contactNumber: new FormControl<number>(0, { nonNullable: false })
   });
}
```

```js
@Component({
    selector: 'app-root',
    template: '{{ title }}',  // Now compiles!
})
export class SampleComponent {
    protected title: string = 'Angular 14';
}
```

# v16
- `.pipe(takeUntilDestroyed())` operator to replace `.pipe(takeUntil($destroyed))`
- Angular signals
- Angular signals easly convert to and from observables
- Standalone projects from start `ng new --standalone`

```js
import {toSignal, toObservable} from '@angular/core/rxjs-interop';

dataSignal = toSignal(this.dataService.data$, []);
dataObservable = toObservable(this.dataSignal);
```

# v17
- beta angular.dev documentation
- new directives for @if, @switch and @for loop
- optional @empty directive on for loop
- @defer directive allow you to lazily load a specific block
- @angular/universal moved into @angular/ssr making it easier to setup and deploy

```js
@if (loggedIn) {
  The user is logged in
} @else {
  The user is not logged in
}
```

```js
@switch (accessLevel) {
  @case ('admin') { <admin-dashboard/> }
  @case ('moderator') { <moderator-dashboard/> }
  @default { <user-dashboard/> }
}
```

```js
@for (user of users; track user.id) {
  {{ user.name }}
} @empty {
  Empty list of users
}
```

```js
@defer (on viewport) {
  <comment-list/>
} @loading {
  Loading…
} @error {
  Loading failed :(
} @placeholder {
  <img src="comments-placeholder.png">
}
```