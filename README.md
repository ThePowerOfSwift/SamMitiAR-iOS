# SamMiti AR on iOS

Ready-and-easy-to-use ARKit framework for the best user experience.

## Overview

Augmented Reality in iOS has been a very big topic since Apple announced ARKit in WWDC 2017. The API has widely used to leverage 3D immersive user experience; however, in order to implement a good ARKit experience, there are a lot of small components to consider, and it takes a lot of time and effort. SamMiti-AR on iOS is an ARKit framework that has been made based on most of the basic user experiences aligning to Apple human interface guidelines and common functions ready for engineers to use.

## Description

SamMiti-AR on iOS has wrapped most of AR-and-3D-related functionalities in one place. That means a lot of time that needs to be spent on the basic structure will be reduced by using this framework. 

For you information, the framework was made on top of ARSCNView (ARKit SceneView) which use SceneKit as an engine to render images, so you can expect a lot of sceneKit functions are referred in this framework.

## Requirement

* iOS 11.0+
* Xcode 9.0+

## Installation

### CocoaPods
SamMitiAR is available through CocoaPods. To install it, simply add the following line to your Podfile:

```ruby
#for iOS 11.0 +
pod 'SamMitiAR', '~> 0.1'

#for iOS 11.3 +
pod 'SamMitiAR', '~> 1.0'
```

## Usage

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus. Aenean eleifend euismod dolor, id tempus eros iaculis et. Aenean efficitur mi id nulla egestas mollis. Integer id tincidunt tortor.

### SamMiti-AR for iOS Structure and How it works

This framework was made on top of ARSCNView which utilizes both functionalities of SceneKit and ARKit. Moreover, the framework has several helper classes to setup the basic necessory augmented reality experience, load and place virtual objects, allow users to interact with the objects. The classes in the framework consist of ......

<Image showing SamMiti structure>

### Setup and Configure

To Use SamMitiARView, after install SamMiti pod, you can simply create new ARSCNView in the storyboard, change the view to subClass to SamMitiView and create IBOutlet linking to your storyboard, or programatically initialize SamMitiARView in your view controller.

<Image showing subclass ARSCNView in story board to SamMitiARView>

In your view controller, you will need to import SamMiti framework along with ARKit and SceneKit.

```swift
import SamMiti
import ARKit
import SceneKit
```

In order to have SamMitiView be able to call back to your view controller, the delegate method need to be defined, and ViewDidLoad function is a good place for it.

```swift
// SamMiti AR View Delegate
sceneView.samMitiARDelegate = self
```

To config some behaviors, you can do that in ViewDidLoad function of view controller. There are a few functions that need to be called before the view is initialied ARSession which includes enabling the camera auto focus function `isAutoFocusEnabled`, .... and serveral optional functions that you can change when the ARSession is running.


```        
// SamMiti AR View Configuration
sceneView.isAutoFocusEnabled = false

// SamMiti AR View Configuration can be changed along the ARSession is running
sceneView.hitTestPlacingPoint = CGPoint(x: 0.5, y: 0.5)
sceneView.isLightingIntensityAutomaticallyUpdated = true
sceneView.baseLightingEnvironmentIntensity = 6
```

To have SamMitiAR run, `setup()` need to be called in View Will Appeare. 

```swift
sceneView.setup(withDebugOptions: [])
```

Besides the `setup()` function, `session.pause()` still needs to be called when view will disappere to stop processing the ARSession when users leave the the view controller.

```swift
// Pause the view's AR session.
sceneView.session.pause()
```

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus.

### Placing and Removing Virtual Objects

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus. 

```swift
func prepareToPlaceVirtualObject() {

    let virtualObjectScene = SCNReferenceNode(named: "art.scnassets/stubhub_model/stadium_1223.scn")!
    let virtualObjectNode = SamMitiVirtualObject(refferenceNode: refNode, allowedAlignments: .all)

    /*
    let virtualObjectGLTFNode = SamMitiVirtualObject(gltfUrl: URL(string: "https://raw.githubusercontent.com/KhronosGroup/glTF-Sample-Models/master/2.0/Duck/glTF-Embedded/Duck.gltf")!, allowedAlignments: [.horizontal])
    */

    SamMitiVitualObjectLoader().loadVirtualObject(virtualObjectNode, loadedHandler: self.handleLoad)

}

func handleLoad(virtualNode: SamMitiVirtualObject?) {

    guard let virtualNode = virtualNode else { return }
    samMitiARView.currentVirtualObject = virtualNode

}
```

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus. 

```swift
func remove(virtualNode: SamMitiVirtualObject?) {

    guard let virtualNode = virtualNode else { return }
    samMitiARView.currentVirtualObject = virtualNode
        
    if samMitiARView.placedVirtualObjects.contains(virtualNode) {
        self.virtualObjectLoader.remove(virtualNode)
    }

}
```

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus. Aenean eleifend euismod dolor, id tempus eros iaculis et. Aenean efficitur mi id nulla egestas mollis. Integer id tincidunt tortor. Nulla semper ornare arcu ullamcorper tincidunt. Aliquam vel accumsan nisl, nec vulputate urna. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Integer libero metus, cursus quis purus nec, viverra tempor turpis. Quisque malesuada quam quis arcu cursus, pretium viverra sapien facilisis.

### Customize Focus Node

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus. 

<Image explain how focus node works>

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus. 

```swift
samMitiARView.focusNode = SamMitiFocusNode(withNotFoundNamed: "art.scnassets/focus_node_not_found.scn",
                                            estimatedNamed: "art.scnassets/focus_node_estimated.scn",
                                            existingNamed: "art.scnassets/focus_node_existing.scn")
```

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus. Aenean eleifend euismod dolor, id tempus eros iaculis et. Aenean efficitur mi id nulla egestas mollis. Integer id tincidunt tortor. Nulla semper ornare arcu ullamcorper tincidunt. Aliquam vel accumsan nisl, nec vulputate urna. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Integer libero metus, cursus quis purus nec, viverra tempor turpis. Quisque malesuada quam quis arcu cursus, pretium viverra sapien facilisis.

### Leverage SamMiti-AR Callbacks

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus. 

```swift
func trackingStateReasonChanged(to trackingStateReason: ARCamera.TrackingState.Reason?) {
    guard let trackingStateReason = trackingStateReason else { return }
    switch trackingStateReason {
    case ARCamera.TrackingState.Reason.excessiveMotion:
        messageLabelDisplay("Please move your phone slower")
    case ARCamera.TrackingState.Reason.initializing:
        messageLabelDisplay("Initializing AR Experience")
    case ARCamera.TrackingState.Reason.insufficientFeatures:
        messageLabelDisplay("Seems like there isn't enough light")
    case ARCamera.TrackingState.Reason.relocalizing:
        messageLabelDisplay("Relocalizing AR Experience")
    }
}
```

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus. 

```swift
func samMitiViewWillPlace(_ virtualObject: SamMitiVirtualObject, at transform: SCNMatrix4) {
    guard let virtualObjectName = virtualObject.name else { return }
    messageLabelDisplay("SamMiti will place \(virtualObjectName)")
    let generator = UIImpactFeedbackGenerator(style: .heavy)
    generator.impactOccurred()
}
```

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis fringilla lectus. Nullam ornare erat eget ultrices rhoncus. 

## Contributing to SamMiti AR

To report a bug or enhancement request, feel free to file an issue under the respective heading.

If you wish to contribute to the project, fork this repo and submit a pull request.

## License

![prolific](https://s3.amazonaws.com/prolificsitestaging/logos/Prolific_Logo_Full_Color.png)

Copyright (c) 2017 Prolific Interactive

SamMiti-AR-iOS is maintained and sponsored by Prolific Interactive. It may be redistributed under the terms specified in the [LICENSE] file.

[LICENSE]: ./LICENSE
