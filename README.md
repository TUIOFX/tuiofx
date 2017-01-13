# TUIOFX

A JavaFX Toolkit for Interactive Tabletops and Surfaces

## Overview

The TUIOFX toolkit aims at supporting Java developers that want to develop for shared interactive surfaces, like multi-user, multi-touch tabletops and walls that support the TUIO protocol.

The TUIOFX toolkit comes with two parts, the TUIOFX-Core and the TUIOFX-WidgetToolkit:

TUIOFX-Core provides an abstraction from the raw TUIO messages and transforms them into standard JavaFX Touch- and Gesture-Events. It uses JavaFX’s multi-touch event handling infrastructure and its predefined TouchEvent and GestureEvent types in order to send events about recognised touches and gesture to the associated target Node (UI element).

TUIOFX-WidgetToolkit optimised JavaFX pre-built look-and-feel for multi-user and multi-touch interaction. For example, UI controls that are adjusted in size for touch on big screens and text-fields that allow simultaneous text-entry through multiple on-screen keyboards. 

## Prerequisites

TUIOFX requires Java 8u45 and a TUIO enabled tracker. TUIOFX further relies on the following libraries:
- TUIO 1.1. Java API
- Simple Logging Facade for Java (SLF4J)
- Guava: Google Core Libraries for Java

## Downloading TUIOFX

- TUIOFX Quickstart
- TUIOFX-Core 
- TUIOFX-All

In order to get an overview ogf the API, please look at the [JavaDoc](http://tuiofx.org/api/index.html)

## Testing with your TUIO-Setup

Both JAR files are runnable by either double-clicking or calling java -jar tuiofx-<version>.jar . Each JAR starts a small demo that allows you to test your TUIO setup. Both demos expect TUIO compatible hardware, delivering TUIO events on the standard port 3333. The TUIO webpage provides a range of trackers, bridges usfecusa and simulators, that can help you with your specific setup. Please mind that you require the needed libraries to start the JARs. 

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

## Your First TUOIFX Application

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
