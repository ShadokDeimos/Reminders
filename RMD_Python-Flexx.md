# PYTHON with FLEXX

## IMPORT and basis render

from flexx import flx

class Example(flx-Widget):

    def init(self):
        with .......

## RENDERING

To create an actual app from a widget, simply wrap it into an App. You can then launch() it as a desktop app, serve() it as a web app, dump() the assets, export() it as a standalone HTML document, or even publish() it online (experimental). Later in this guide we dive deeper into the different ways that you can run your app.

### In WebBrowser

app = flx.App(Example)
app.export('example.html', link=0)  # Export to single file

### In App

app = flx.App(Example)

app.launch('app')  # to run as a desktop app
# app.launch('browser')  # to open in the browser
flx.run()  # mainloop will exit when the app is closed

## WIDGETS

### Generate button

class Example(flx.Widget):

    def init(self):
        flx.Button(text='hello')
        flx.Button(text='world')


### Generate button using flex display properties

class Example(flx.Widget):

    def init(self):
        with flx.HBox():
            flx.Button(text='hello', flex=1)
            flx.Button(text='world', flex=2)


### Divise display

class Example(flx.Widget):

    def init(self):
        with flx.HSplit():
            flx.Button(text='foo')
            with flx.VBox():
                flx.Widget(style='background:red;', flex=1)
                flx.Widget(style='background:blue;', flex=1)

## Flexx Components

### PyComponent and JsComponent

A Flexx app consists of components that exist in either Python or JS, and which can communicate with each-other in a variety of ways

The PyComponent and JsComponent classes derive from the Component class.

To know :
- They are both associated with a Session
- They have an id attribute that is unique within their session, and a uid attribute that is globally unique
- They live (their methods run) in Python and JS, respectively
- A PyComponent can only be instantiated in Python, a JsComponent can be instantiated in both Python and JavaScript
- A PyComponent always has a corresponding proxy object in JS
- A JsComponent may have a proxy object in Python; these proxy objects are created automatically when Python references the component

### Proxy Components

### The root component

## WIDGETS CLASSES LIST

### Base Widgets

Widget

### Layouts

FormLayout
HBox
HFix
HSplit                        Horizontal split
HVLayout
Layout
PinboardLayout
StackLayout
TabLayout
VBox
VFix
VSplit                        Vertical split

### Widgets

BaseButton
BokehWidget
Button
CanvasWidget
CheckBox
ColorSelectWidget
ComboBox
DropdownContainer
GroupWidget
IFrame
ImageWidget
Label
LineEdit
PlotWidget
PlotlyWidget
ProgressBar
RadioButton
RangeSlider
Slider
ToggleButton
TreeItem
TreeWidget
VideoWidget
Widget
YoutubeWidget
