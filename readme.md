<p align="center">
  <img src="/logo.png" width="250">
</p>
<p align="center" style="margin-top: 40px">
  <strong>Ngx-App-Tour</strong>
</p>
<p align="center">
  <a href="https://hamdiwanis.github.io/ngx-app-tour">Demo</a>
</p>

> This library built on the great lib ngx-tour by [isaacplmann](https://github.com/isaacplmann.)  It also uses the popover component by my favourite angular ui lib [ng-zorro-antd](https://github.com/NG-ZORRO/ng-zorro-antd).

### Installation

```
npm install ngx-app-tour
```

Add lib styles to your app for ex styles in angular.json:
```
"styles": [
              "node_modules/ngx-app-tour/styles/styles.css",
             ...
            ],
```

###  Usage
Add in your root module:
```
@NgModule({
  imports: [
    ...
    NgxAppTour.forRoot()
  ],
})
export class AppModule { }
```

Add in every other module you use it in:
```
@NgModule({
  imports: [
    ...
    NgxAppTour
  ],
})
export class AppModule { }
```

Add in every other module you use it in:
```
@NgModule({
  imports: [
    ...
    NgxAppTour
  ],
})
export class AppModule { }
```

Mark your tour steps with tourAnchor and give it an id:
```
<div tourAnchor="id"></div>
```

Enject TourService in a component:
```
constructor(public tourService: TourService) {}
```

Use the TourService to init tour tour:
```
this.tourService.initialize(steps[], defaults);
```

Use the TourService to control the tour:
```
this.tourService.start();
this.tourService.stop();
this.tourService.pause();
this.tourService.resume();
```

Use the TourService to listen for tour events:
```
this.tourService.events$.subscribe(e => do something)
```

Use custom step template:
```
<ng-template #stepTemplate let-step="step">
    <div class="step-container">
        <div class="custom-step-content">
            {{ step?.content }}
        </div>
        <div class="step-actions">
            <button class="step-btn" [disabled]="!tourService.hasPrev(step)" (click)="tourService.prev()">
                prev
            </button>
            <button class="step-btn" [disabled]="!tourService.hasNext(step)" (click)="tourService.next()">
                next
            </button>
            <button class="step-btn" (click)="tourService.end()">{{ step?.endBtnTitle }}</button>
        </div>
    </div>
</ng-template>
```

```
    @ViewChild('stepTemplate') stepTemplate;
 
    // then use it with a single step
    this.tourService.initialize([
       ...
       {
        ...
         stepTemplate: this.stepTemplate
       },
       ...
     ]);
     
     // or as default template
     
     this.tourService.initialize([...], {stepTemplate: this.stepTemplate});
     
```

Use touranchor--is-active class to style active step:
```
.touranchor--is-active{
    // your styles
}
```


### Tour Step Options
```
export interface IStepOption {
  stepId?: string;
  anchorId?: string;
  title?: string;
  content?: string;
  route?: string | string[] | UrlSegment[];
  nextStep?: number | string;
  prevStep?: number | string;
  preventScrolling?: boolean;
  prevBtnTitle?: string;
  nextBtnTitle?: string;
  endBtnTitle?: string;
  disableBackdrop?: boolean;
  backdropColor?: string;
  backdropRadius?: string;
  /* Add ripple effect tour target */
  enableRippleEffect?: boolean;
  rippleColor?: string;
  /* Change step default template */
  stepTemplate?;
  /*  Use this to allow click, type..etc on tour target */
  allowInteractions?: boolean; // true if you set a nextOn
  /*  se this to wait for certn event on step target before going to the next step 
      like click on a button or hit enter on an input */
  nextOn?: string; // disable next btn on default template
  placement?: 'topLeft' | 'top' | 'topRight' | 'leftTop' | 'left' | 'leftBottom'
    | 'rightTop' | 'right'| 'rightBottom'| 'bottomLeft' | 'bottom'| 'bottomRight';
}
```

###Changes

```
Version 1.2.0

*Add allowInteractions option on tour step
-> Use this to allow click, type..etc on tour target
*Add allowInteractions nextOn on tour step
-> Use this to wait for certn event on step target before going to the next step 
like click on a button or hit enter on an input
```
