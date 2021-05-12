# megamtech-labs/ngx-daterangepicker

 Megamtech Daterange picker for angular 6+.


This `Megamtech Daterange picker` plugin is compatible with Angular 6+ and is Ivy compatible. It leverages `date-fns` to handle date manipulation and parsing. 

![image-1.png](./image-1.png)

---




## Installation

 Install the plugin from npm:

 `npm i @megamtech-labs/ngx-datepicker --save` .

 import **ngxDaterangepicker** in your module:

````typescript
...
import { FormsModule } from '@angular/forms';
import { ngxDaterangepicker } from '@megamtech-labs/ngx-datepicker';
import { App } from './app';

@NgModule({
    imports: [
        ... ,
        FormsModule,
       ngxDaterangepicker.forRoot({
      applyLabel: 'Okay',
      firstDay: 3
    })
    ],
    declarations: [App],
    bootstrap:    [App]
})
export class AppModule {}
````

## Usage example

Html:

```html
<input type="text" ngxDaterangepicker [(ngModel)]="selected" class="form-control"/>
```
Typescript:

````typescript
selected: {startDate: startOfDay(new Date()), endDate: endOfDay(new Date())};
````
### with some options:
Html:

```html
<input type="text" matInput
    ngxDaterangepicker
    [locale]="{applyLabel: 'ok', format: 'DD-MM-YYYY'}"
    startKey="start"
    endKey="end"
    [(ngModel)]="selected"
    name="daterange"/>
```
Typescript:

````typescript
selected: {startDate: startOfDay(new Date()), endDate: endOfDay(new Date())};
````


## Inline usage

You can use the component directly in your templates, which will set its `inline` mode to **true**, in which case the calendar won't hide after date/range selection. You can then use the events: `rangeClicked` or `datesUpdated` or `choosedDate` to get its selection state.

```html
<ngx-daterangepicker-material (choosedDate)="choosedDate($event)">
</ngx-daterangepicker-material>
```


## Available options

### autoApply, showDropdowns, singleDatePicker, showWeekNumbers, showISOWeekNumbers, alwaysShowCalendars, showClearButton, showCancel

>These options are booleans

### isCustomDate

>(function) A function that is passed each date in the calendars before they are displayed, and may return a string or array of CSS class names to apply to that date's calendar cell

### isInvalidDate
>(function) A function that is passed each date in the two calendars before they are displayed, and may return true or false to indicate whether that date should be available for selection or not.

### isTooltipDate
>(function) A function that is passed each date in the two calendars before they are displayed, and may return a text to be displayed as a tooltip.

### minDate, maxDate

 >To set the minimal and maximal date, these options are a moment date

### dateLimit

 >To set max number of the date we can choose

### locale

>the locale options is an object with:
```javascript
{
    format: 'MM/DD/YYYY', // could be 'YYYY-MM-DDTHH:mm:ss.SSSSZ'
    displayFormat: 'MM/DD/YYYY', // default is format value
    direction: 'ltr', // could be rtl
    weekLabel: 'W',
    separator: ' To ', // default is ' - '
    cancelLabel: 'Cancel', // detault is 'Cancel'
    applyLabel: 'Okay', // detault is 'Apply'
    clearLabel: 'Clear', // detault is 'Clear'
    customRangeLabel: 'Custom range',
    firstDay: 1 // first day is monday
}
```

### startKey and endKey

Theses 2 options are for the key you want for the value, default are `startDate` and `endDate`, it means the value we have from ngModel are: `{startDate: Date, endDate: Date}` by default;

Specifiyng `startKey` and `endKey` would have different model:

example:
```html
<input type="text" ngxDaterangepicker startKey="start" endKey="end" [(ngModel)]="model">
```

the model we got would be:  `{start: Date, end: Date}`

### ranges

(object) Set predefined date ranges the user can select from. Each key is the label for the range, and its value an array with two dates representing the bounds of the range. As an example:
```html
<input type="text" ngxDaterangepicker startKey="start" endKey="end" [ranges]="ranges" [(ngModel)]="model">
```
```typescript
ranges: any = [
    { label: 'Today', start: startOfDay(new Date()), end: endOfDay(new Date()) },
    { label: 'Yesterday', start: startOfDay(sub(new Date, { 'days': 1 })),
     end: endOfDay(sub(new Date, { 'days': 1 })) },
    { label: 'Last 7 Days', start: startOfDay(sub(new Date, { 'days': 7 })), end: endOfDay(new Date()) },
    { label: 'Last 30 Days', start: startOfDay(sub(new Date, { 'days': 30 })), end: endOfDay(new Date()) },
    { label: 'This Month', start: startOfMonth(new Date), end: endOfDay(new Date()) },
    { label: 'Last Month', start: startOfMonth(sub(new Date, { months: 1 })),
     end: endOfMonth(sub(new Date, { months: 1 })) },
    { label: 'Last 3 Month', start: startOfMonth(sub(new Date, { months: 3 })), 
    end: endOfMonth(sub(new Date, { months: 1 })) }
]
```
#### Other options with ranges

You can use bellow options when using the ranges. The default are `false`.

| Attribut | Type |Description |
| --- | --- |--- |
| alwaysShowCalendars | boolean | set to `true` if you want to display the ranges with the calendar |
| keepCalendarOpeningWithRange | boolean | set to `true` if you want the calendar won't be closed after choosing a range |
| showRangeLabelOnInput | boolean | set to `true` if you want to display the range label on input |
| customRangeDirection | boolean | set to `true` if you want to allow selection range from end date first |
| lockStartDate | boolean | set to `true` if you want to lock start date and change only the end date |

#### Open datepicker from outside

It is possible to open datepicker from outside. You should create an input with attached datepicker directive and a button with "ngx-daterangepicker-action" class (to prevent triggering of clickOutside).
```html
    <input
      ngxDaterangepicker
      [closeOnAutoApply]="true"
      [autoApply]="true"
      [singleDatePicker]="true"
      [linkedCalendars]="true"
      [(ngModel)]="selected"
      (datesUpdated)="datesUpdated($event)"
      class="datepicker-calendar-icon">

    <a class="ngx-daterangepicker-action" (click)="openDatepicker()">
      Open
    </a>
```



### Timepicker

You have to set the attribute `timePicker` to `true` if you want to enable the timepicker.

You can use theses options:

| Attribut | Type |Description |
| --- | --- |--- |
| timePicker24Hour | boolean | set to `true` if you want to set the timepicker to 24h instead of having AM and PM |
| timePickerIncrement | number | set the value increment of the minutes (eg: for `12` there would be 0mn, 15mn, 30mn, 45mn,) |
| timePickerSeconds | boolean | set `true` if you want do display second's select |


### Customisation

| Attribut | Type |Description |
| --- | --- |--- |
| firstMonthDayClass | string | add a custom class for all first day of the month |
| lastMonthDayClass | string | add a custom class for all last day of the month |
| emptyWeekRowClass | string | add a custom class in a row with a date in a week not in the current month |
| emptyWeekColumnClass | string | add a custom class for all date in a week not in the current month |
| lastDayOfPreviousMonthClass | string | add a custom class for the last day of the previous month |
| firstDayOfNextMonthClass | string | add a custom class for the first day of the next month |

### Positioning

| Attribut | Possible values |Description |
| --- | --- |--- |
| opens | left, center, right | position the calendar from the input element |
| drops | up, down | position the calendar to the up or down of the calendar |

## Available events

### \(rangeClicked)

 >Fired when clicked on range, and send an object with range label and dates value, eg:  `{label: 'This Month', dates: [Date, Date]}`

### \(datesUpdated)

 >Fires when the date model is updated, like applying (if you have activated the apply button), or when selecting a range or date without the apply button, and sends an object containing start and end dates, eg: `{startDate: Date, endDate: Date}`

### Global locale

For setting the global locale, pass this object to ngxDaterangepicker.forRoot().

eg:

```
@NgModule({
    imports: [
        ... ,
        FormsModule,
        ngxDaterangepicker.forRoot({
            separator: ' - ',
            applyLabel: 'Okay',
        })
    ],
    declarations: [App],
    bootstrap:    [App]
})
```

## Development

### Prepare your environment

Install local dependencies: `npm install`.

### Development server

Run `npm start` to start a development server on a port 4401.

Open `http//:localhost:4401` on your browser.

## Tests

Run `npm test` or `ng test` to run tests.



MIT
