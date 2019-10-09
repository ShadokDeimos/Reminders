# ANGULAR 6

## INSTALL ANGULAR

npm install -g @angular/cli@version

## CREATE PROJECT

ng new app-name

## RUN ANGULAR

-> Dev environment
ng server --env=dev

## CREATE COMPONENT

ng generate component example

### example.component.ts

`@Component({                  Decorator function that specifies Angular metadata for component
  selector: 'app-heroes',     // component's CSS element selector
  templateUrl: './heroes.component.html',   // location of the component's template file
  styleUrls: ['./heroes.component.css']   // location of css styles
})`

/!\ The CSS element selector     => matches the name of the HTML element that identifies this component within a parent component's template

/!\ The ngOnInit      => is a lifecycle hook. Angular calls ngOnInit shortly after creating a component. It's a good place to put initialization logic.

## HTML lists

### List an element from component

`<li *ngFor="let hero of heroes">
  <span class="badge">{{hero.id}}</span> {{hero.name}}
</li>`

## LIFECYCLE HOOKS

* ngOnChanges()   
        =>  Respond when (re)sets data-bound input properties
        =>  Receive a SimpleChanges object of current and previous property values
        =>  Called before ngOnInit()

* ngOnInit()
        =>  Initialize the directive/component after first display the data-bound properties
        =>  Called once, after first ngOnChanges()

* ngDoCheck()
        =>  Detect and act on changes that Angular can't or won't detect
        =>  Called during every change detection
        =>  Called immediately after ngOnChanges() and ngOnInit()

* ngAfterContentInit()
        =>  Respond after Angular projects extarnal content into  the (component) view that a diretive is in
        =>  Called once after the dirst ngDoCheck()

* ngAfterContentChecked()
        =>  Respond after Angular checks the content projected into the directive/component
        =>  Called after ngAfterContentInit() and every subsequent ngDoCheck()

* ngAfterViewInit()
        =>  Respond after Angular initializes the component's views
        =>  Called once after the first ngAfterContentChecked()

* ngAfterViewChecked()
        =>  Like ngAfterViewInit()
        =>  Called after ngAfterViewInit and every subsequent ngAfterContentChecked()

* ngOnDestroy()
        =>  Cleanup just before Angular destroys the directive/component. Unsubscribe Observables and detach event handlers to avoid memory leaks

## COMPONENTS ARGUMENTS

@Input() var: type;           Allow a component to receive data from its parent
@Output() var: type;          Allow a component to send data to its parent
