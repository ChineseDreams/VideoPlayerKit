VideoPlayerKit
==============

We know how hard making a custom video player is. That's why we created VideoPlayerKit. Using VideoPlayerKit is easy to use. All controls, progress bar, and airplay are already set up to make everyone's life easier.

References to IGN's ShareThis repo and share button to handle sharing are currently commented out. More information can be found [here](https://github.com/ign/ShareThis).

Use the sample project to see how VideoPlayerKit works.

An example from IGN Pro League's deprecated "IPL" app (with ShareThis) are shown below:

[![](http://i.imgur.com/Ayxdp5V.png)](http://i.imgur.com/Ayxdp5V.png)
[![](http://i.imgur.com/KNIxaWr.png)](http://i.imgur.com/KNIxaWr.png)

[![](http://i.imgur.com/disgBRz.png)](http://i.imgur.com/disgBRz.png)
[![](http://i.imgur.com/v4WswEi.png)](http://i.imgur.com/v4WswEi.png)

# Using the sample project
Download the github project and use the Makefile to gather all the pods require for VideoPlayerKit. Use the following command:
``` objective-c
make clean setup
```

Note: If you get a build error due to architectural dependencies, update the following value in your
Pods project's Build Settings for both Debug and Release modes:
``` objective-c
Set Build Active Architectures Only —> “No”
```

# Installation Instructions:

## In the View Controller that will contain the video player:

### Import VideoPlayerKit.h
``` objective-c
import "VideoPlayerKit.h"
```

### Initializing video player
``` objective-c
[VideoPlayerKit initWithContainingViewController:optionalTopView:hideTopViewWithControls:];
[VideoPlayerKit initWithContainingView:optionalTopView:hideTopViewWithControls:];
```
Make sure that the view controller, or a specific inline view for inline players, containing the video player is passed into the first parameter. The optional top view is a view that will be at the top of the video player. This can be use to put any additional buttons or labels. The third parameter is a boolean that will be used to check if the top view should hide with the video player controls. If this is set to NO, it is still possible to hide the top view only on certain times given the situation using the two notifications: kVideoPlayerWillHideControlsNotification and kVideoPlayerWillShowControlsNotification.

### Top View Edge Inset
``` objective-c
setControlsEdgeInsets
```
If a top view is set, use this to offset the controls so it accounts for the top view. Usually you'll only want to change the edge inset's top parameter but the option is left open to change it entirely.

### Playing the video
``` objective-c
playVideoWithTitle:URL:videoID:isStreaming:playInFullScreen:
```
The method will automatically initialize the video player and start playing the video that is given in the url. The title parameter is used for the label that will appear near the top of the video player under the optional Top View. The videoID and isStreaming parameters are used mainly for analytics tracking. The last parameter, playInFullScreen, is a boolean that when set to YES, the video will play automatically in fullscreen without an inline player.

## VideoPlayerDelegate

### Event tracking
``` objective-c
trackEvent:videoID:title:
```
This method is used for analytic event tracking. The first parameter will be one of three events: kTrackEventVideoStart, kTrackEventVideoLiveStart, kTrackEventVideoComplete. The videoID and title will be the same ones that was passed into the method playVideoWithTitle:URL:videoID:isStreaming:playInFullScreen:

### Fullscreen toggle switch
``` objective-c
BOOL fullScreenToggled
```
This property will be set to YES whenever the video player is fullscreen modally.

## Optional Methods

### Launch video player in fullscreen
``` objective-c
launchFullScreen
```

### Minimize video player from fullscreen
``` objective-c
minimizeVideo
```

### Play and pause video
``` objective-c
playPauseHandler
```
Plays the video if paused. Pauses the video if playing.

## Optional properties

### Check if fullscreen mode is toggled
``` objective-c
fullScreenModeToggled
```

### Set the end time to static or dynamic
``` objective-c
showStaticEndTime
```
Set this boolean to YES if the end time should just be a static label. Default setting is NO which will make the end time decrease as the video plays.

### Get current video info
``` objective-c
currentVideoInfo
```
A dictionary which uses these keys: @"title" for title of video, @"videoID" for id of video, @"isStreaming" to check if it is a live video.

### Check if video is playing
``` objective-c
isPlaying
```

### Allow fullscreen view to be in portrait
``` objective-c
allowPortraitFullscreen
```
Default fullscreen is landscape. For portrait fullscreen, mark this property to YES.

# License
ShareThis is available under the MIT license. See the LICENSE file for more info.
