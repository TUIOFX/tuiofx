# TUIOFX

A JavaFX Toolkit for Interactive Tabletops and Surfaces

[![tuiofx video](https://i.vimeocdn.com/video/521075838_640.jpg)](https://vimeo.com/129548709)


## Introduction

The TUIOFX toolkit aims at supporting Java developers that want to develop for shared interactive surfaces, like multi-user, multi-touch tabletops and walls that support the TUIO protocol.

The TUIOFX toolkit comes with two parts, the **TUIOFX-Core** and the **TUIOFX-WidgetToolkit**:

**TUIOFX-Core** provides an abstraction from the raw TUIO messages and transforms them into standard JavaFX Touch- and Gesture-Events. It uses JavaFX’s multi-touch event handling infrastructure and its predefined TouchEvent and GestureEvent types in order to send events about recognised touches and gesture to the associated target Node (UI element).

**TUIOFX-WidgetToolkit** optimised JavaFX pre-built look-and-feel for multi-user and multi-touch interaction. For example, UI controls that are adjusted in size for touch on big screens and text-fields that allow simultaneous text-entry through multiple on-screen keyboards. 

## Prerequisites

TUIOFX was tested with Java 8u45 and requires a TUIO enabled tracker. TUIOFX further relies on the following libraries:
- [TUIO 1.1. Java API](https://github.com/mkalten/TUIO11_JAVA)
- Simple Logging Facade for Java (SLF4J)
- Guava: Google Core Libraries for Java

## Downloading TUIOFX

Below are all currently available downloads for the latest development version of TUIOFX (v0.10.4). There is not yet a stable version.

- [TUIOFX Quickstart](https://github.com/TUIOFX/tuiofx/releases/download/0.10.4/tuiofx_quickstart.zip)
    - Eclipse Project with 3 examples and all required libraries and dependencies
- [TUIOFX-Core](https://github.com/TUIOFX/tuiofx/releases/download/0.10.4/tuiofx-core-0.10.4.jar) 
    - JAR including TUIOFX-Core only
- [TUIOFX-All](https://github.com/TUIOFX/tuiofx/releases/download/0.10.4/tuiofx-all-0.10.4.jar)
    - JAR including TUIOFX-Core and TUIOFX-WidgetToolkit

In order to get an overview ogf the API, please look at the [JavaDoc](http://tuiofx.org/api/index.html)

## Testing with your TUIO-Setup

Both JAR files are runnable by either double-clicking or calling ```java -jar tuiofx-<version>.jar```. Each JAR starts a small demo that allows you to test your TUIO setup. Both demos expect TUIO compatible hardware, delivering TUIO events on the standard port 3333. The [TUIO webpage](http://www.tuio.org/?software) provides a range of trackers, bridges, and simulators, that can help you with your specific setup. If you do not have a TUIO setup yet, we can recommend [Tongseng](https://github.com/fajran/tongseng) for testing with Apple multi-touch trackpads, and [TuioDroid](https://github.com/TobiasSchwirten/tuiodroid) and [TuioPad](http://www.memo.tv/tuiopad/) for testing with Android or iOS devices. Please mind that you require the needed libraries to start the JARs.

Please mind, if your multi-touch hardware also sends native gesture- and touchevents (e.g. Windows Touch) besides TUIO events, to disable  the sending of native events.

## Using TUIOFX in your Code

After downloading TUIOFX jars and dependencies, add or import the required jars to your JavaFX project. Alternatively start with the Quickstart project. In your code, initialize TUIOFX before launching your JavaFX application. Typically this is done in your main method: 
```java
public class TuioFXApplication extends Application {
    //...
        public static void main(String[] args) {
            TuioFX.enableJavaFXTouchProperties();
            launch(args);
        }
    //...
}
```
Now, create a TUIOFX instance by passing over the JavaFX stage that should react to TUIO inputs from your TUIO tracker, and a Configuration . 
```java
TuioFX tuioFX = new TuioFX(stage, Configuration.default());
```
Optionally, you can include TUIOFX-WidgetToolkit: 
```java
tuioFX.enableMTWidgets(true);
```
Finally, start the TUIOFX instance to react to TUIO input: 
```java
tuioFX.start();
```
Note: The class Configuration allows to customise some parameters to optimise TUIOFX for specific hardware or make application specific settings - with several presets at hand. Among the parameters that can be influenced are the duration of a long press, the detection of swipes, etc. Via the Configuration and Configuration.Builder it is also possbile to toggle the visualisation of detected touches and the debug output. 

## Your First TUIOFX Application

Here is a simple example that illustrates the usage of TUIOFX in a JavaFX application: 

```java
public class TuioFXApplication extends Application {

    public static void main(String[] args) {
        TuioFX.enableJavaFXTouchProperties();
        launch(args);
    }

    @Override
    public void start(Stage stage) throws Exception {
        Pane root = new StackPane();
        Scene scene = new Scene(root);
        stage.setScene(scene);

        // start TuioFX
        TuioFX tuioFX = new TuioFX(stage, Configuration.debug());
        tuioFX.enableMTWidgets(true);
        tuioFX.start();

        // display application window
        stage.show();
    }
}
```

Download a simple Hello World example [here](http://tuiofx.org/files/HelloTUIOFX.java). The example displays a Label which can be scaled, rotated, and moved with mutli-touch gestures. 

## TUIOFX Properties

TUIOFX gives you some finer controlled over some behaviours by using properties. 

### The isTUIOTouchTransparent-Property

Sometimes it is necessary to make some nodes transparent for receiving touch inputs. One example are components like ```HBox``` or ```VBox``` you only need for layouting. If you want such components not to interfere with the listeners of parent nodes, you can use the ```isTouchTransparent```-Property to make a component 'invisible' for touch-events that are send through TUIOFX. 

```java
hbox.getProperties().put("isTouchTransparent", "true"); 
```
This property can also be set in Scene Builder for an FXML file. 

### The focusArea-Property

Allows to set a Task-based focus for groups of widgets that are used by one user in multi-user enviroments. Detailed instructions are coming later!

```java
hbox.getProperties().put("focusArea", "true"); 
```
The usefocusArea-property allows for further adjustments. It allows to specify for single elements, if it should ignore any focus areas set in parent elements. 

```java
text.getProperties().put("usefocusArea", "false"); 
```
Both properties can also be set in Scene Builder for an FXML file.

## Publications
- Fetter, M., Bimamisa, D. and Gross, T. TUIOFX - A JavaFX Toolkit for Shared Interactive Surfaces. Proceedings of the ACM on Human-Computer Interaction 1, 1 (June 2017). pp. 9:1-9:18. (ISSN: 2573-0142). 
- Fetter, M., Bimamisa, D. and Gross, T. [Task-Based Focus and AdHoc-Focus-Territory—Novel Concepts for Shared Interactive Surfaces](http://dl.acm.org/citation.cfm?doid=2851581.2892446). In Extended Abstracts of the Conference on Human Factors in Computing Systems – CHI 2016 (May 7-12, San Jose, CA, USA). ACM Press, New York, NY, USA, 2016. pp. 1193-1200.  
- Fetter, M., Bimamisa, D. and Gross, T. [Plattformübergreifende Interaktive Tischanwendungen mittels TUIOFX](http://cml.hci.uni-bamberg.de/publ/mc15_fetter_et_al_TUIOFX.pdf) (Platform-Independent Applications for Interactive Tables with TUIOFX; in German). In 15. Fachuebergreifende Konferenz fuer interaktive und kooperative Medien - M&C 2015 (Sept. 6-9, Stuttgart, Germany). Walter de Gruyter GmbH, Berlin/Boston, 2015. pp. 359-362.(ISBN: 987-3-11-044334-9). Honorable Mention Poster Award
- Fetter, M. and Bimamisa, D. [TUIOFX—Toolkit Support for the Development of JavaFX Applications for Interactive Tabletops](http://link.springer.com/chapter/10.1007%2F978-3-319-22723-8_44#page-1). In Proceedings of the 15th IFIP TC.13 International Conference on Human-Computer Interaction - INTERACT 2015 (Sept. 14-18, Bamberg, Germany). Springer, Heidelberg, Germany, 2015. pp. 476-479. 
