# Step By Step Guide for Component Exercise

* Follow Angular Setup Instruction to get project setup.
* Update app.html
  * Remove existing code. Add header element with Women Who Code RVA heading.
  * Add style to app-component.css to style the header. Use this class to style the header.
```css
.wwc-header {
    background-color: #1abc9c;
    color: #5f5f5f;
    height: 150px;
    text-align: center;
    padding-top: 20px;
    padding-bottom: 60px;
    font-size: 35pt;
}
```
## Adding new component
* Generate new component named ‘Community’ using Angular CLI. In command prompt run following command
```
ng generate component Community
```
 Notice that in addition to new files created in directory named ‘Community’, Angular CLI has also updated your app.module.ts file. Check out this file and see what’s updated
* Update community.component.ts file
  * Remove existing ```<p>``` tag and add a ```<div>``` tag with text “Angular Community”
* Update app.component.html file to add tag <app-community>. 
```html
<app-community></app-community>
```
Notice that in community.component.ts file, in @Component decorator the selector is specified as 'app-community'. That's how angular ties ```<app-community>``` tag to our CommunityComponent.

__Checkpoint: Your application should display Angular Community__
Optional: add some css to community.component.css to add some broder and margins.

## Passing data from parent component

So far our CommunityComponent class is very specific. Every consumer of this component will always get "Angular Community". We want comsumer of this component (i.e. parent component) to decide what kind of community they want. That means parent component has to pass the name of the community to CommunityComponent.
* Modify community.component.ts file to add @Input() decorator to the name property. @Input() decorator tells Angular that our component expects the property "name" to be passed in.
```Typescript
@Input()
name:string;
```
* Modify app.component.html to update ```<app-community>``` tag
```html
<app-community name="Angular Community"></app-community>
```
__Checkpoint: You should still see same webpage. Modify name property in the app-community tag and see the difference in the browser.__

* Let's quickly add few more communities. Modify app.component.html to add few more ```<app-communitiy>``` tags

```html
<app-community name="Angular Community"></app-community>
<app-community name="FrontEnd Community"></app-community>
<app-community name="Clean Code Community"></app-community>
<app-community name="Algorithm Community"></app-community>
```

## Use In-built directives *ngFor

Angular provides *ngFor directive to iterate over list and repeatedly display an element. Let's use it to display ```<app-communities>``` tags based on the list of communities we provide.

* Modify AppComponent class in app.component.ts file to add property named 'communities' and initialize in ngOnInit function.

```Typescript
export class AppComponent implements OnInit {
  public communities : string[];
  ngOnInit() {
    this.communities = ["Angular","Front End","Algorithms","Clean Code","Java"];
  }
}
```
* Modify app.component.html. Replace all ```<app-communitiy>``` tags with following code

```html
<app-community *ngFor="let name of communities" name="{{name}}"<app-community>
```

## Property Binding 

So far we have been displaying the values using {{}} syntax. This is called <i>interpolation</i>. Value inside {{ }} is calculated and results are displayed. Now let's try different way called <i>property binding</i>. 
* Update <app-community> tag in app.component.html file 

```html
 <app-community *ngFor="let name of communities" [name]="name"<app-community>
```

## Event Binding
We have bind the property from our component classes to the html tags using either interpolation or property binding. Now let's try to implement event binding, i.e. functions that runs when some event happen. We will add a button and write a function that will run when the button is clicked.

* Modify community.component.html to add a button

```html
<input type="button" [value]="btnValue" (click)="changeInterest()" />
```
* Modify community.component.ts to add the property btnValue that will provide value to the button and method changeInterest that will run when button is clicked.

```Typescript
private btnValue:string;
```

```Typescript
ngOnInit() {
    this.btnValue = "Add";
  }
  changeInterest(){
    this.btnValue = this.btnValue =="Add" ? "Remove" : "Add"; 
}
```
__Checkpoint: Clicking button should change the text on the button.__


## Pass an Event from child component to parent component

So far there in only one way of communication between parent and child. Parent (AppComponent) is sending data to child component (CommunityComponent) and child component is displaying it. Now let’s try the communication from child to parent. Child component talk to parent by emitting events. We emit event to parent using @Output() decorator. 

* Add following to community.component.ts

```Typescript
@Output()
changedInterest = new EventEmitter();
```
* Modify changedInterest() method in community.component.ts to emit changedInterest event

```Typescript
changeInterest(){
    this.changedInterest.emit(this.btnValue ==="Add" ? true : false);
    this.btnValue = this.btnValue =="Add" ? "Remove" : "Add";
  }
```

* Modify ```<app-community>``` tag in app.component.html file to capture the changedInterest event and specify event handler. Here ```$event``` will capure whatever data the child component has passed.

```html
<app-community [name]="community.name" (changedInterest)="updateInterest($event, community)"></app-community>
```

* Modify app.component.ts to add updateInterest function.

```Typescript
updateInterest(event, item){
      item.memberInterested = event;
}
```
* Let's add some css class based on memberInterested propery, so that we can see these changes visually. Angular provides directive called ngClass where we can add css classes conditionally. Modify ```<div>``` tag with *ngFor in app.component.html

```html
<div *ngFor="let community of communities" [ngClass]="{'interested':community.memberInterested, 'notInterested':!community.memberInterested}">
```

* Modify app.component.css to add these two classes

```css
.interested {
    margin-left: 60vw;
    transition: margin 4s;
}

.notInterested {
    margin-left: 0;
    transition: margin 4s;
}

```
__Checkpoint: Checkout your application. Event sent by community component is captured by parent component and that is used to set some css class on parent element.__

___
In this exercise we have covered

  1. Creating new component using Angular CLI
  2. Using interpolation and property binding to pass the data to the template
  3. Using @Input() decorator to pass the data to the child component
  4. Event binding
  5. Using @Output decorator to emit event to parent component
___