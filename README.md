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

Below are all currently available downloads for the latest development version of TUIOFX (v0.10.4). There is not yet a stable version. 

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
