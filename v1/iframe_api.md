# LiveCapTV iFrame API

## Regards

The design of LiveCapTV iFrame API strongly resembles [YouTube iFrame API](https://developers.google.com/youtube/iframe_api_reference) because we want to provide developers with a similar experience like using YouTube Embedded Player APIs.

## Getting Started

## Loading a video player

After the API's JavaScript code loads, the API will call the `onLiveCapIframeAPIReady` function, at which point you can construct a LiveCap.Player object to insert a video player on your page. Example shows below:

	var player;
	function onLiveCapIframeAPIReady() {
		player = new LiveCap.Player(
			'player',
			{
				height: '390',
				width: '640',
				videoId: 'uLMjA0PqyDe',
				events: {
					'onReady': onPlayerReady,
					'onStateChange': onPlayerStateChange
			    }
			}
		);
	}

The constructor for the video player specifies the following parameters:

1. The first parameter specifies either the DOM element or the `id` of the HTML element where the API will insert the `<iframe>` tag containing the player.

The IFrame API will replace the specified element with the `<iframe>` element containing the player. This could affect the layout of your page if the element being replaced has a different display style than the inserted `<iframe>` element. By default, an `<iframe>` displays as an inline-block element.

2. The second parameter is an object that specifies player options. The object contains the following properties:

  - `width` (number) – The width of the video player. The default value is `640`.
  - `height` (number) – The height of the video player. The default value is `390`.
  - `videoId` (string) – The LiveCap video ID that identifies the video that the player will load.
  - `playerVars` (object) – The object's properties identify [player parameters](/v1/player.md) that can be used to customize the player.
  - `events` (object) – The object's properties identify the events that the API fires and the functions (event listeners) that the API will call when those events occur. In the example, the constructor indicates that the `onPlayerReady` function will execute when the `onReady` event fires and that the `onPlayerStateChange` function will execute when the `onStateChange` event fires.

As mentioned in the [Embedded Player](/v1/player.md) section, instead of writing an empty `<div>` element on your page, which the player API's JavaScript code will then replace with an `<iframe>` element, you could create the `<iframe>` tag yourself.

	<iframe src="https://www.livecap.tv/s/embed/riotgames/uLMjA0PqyDe?autoplay=1" width="640" height="360" frameborder="0"></iframe>

If you do write the `<iframe>` tag, then when you construct the `LiveCap.Player` object, you do not need to specify values for the width and height, which are specified as attributes of the `<iframe>` tag, or the `videoId` and player parameters, which are are specified in the src URL. As an extra security measure, you should also include the `origin` parameter to the URL, specifying the URL scheme (http:// or https://) and full domain of your host page as the parameter value. While `origin` is optional, including it protects against malicious third-party JavaScript being injected into your page and hijacking control of your LiveCap player.

## Operations

To call the player API methods, you must first get a reference to the player object you wish to control. You obtain the reference by creating a `LiveCap.Player` object as discussed in the Loading a video player sections of this document.

## Functions

### Playing a video

- `player.playVideo():Void`

  - Plays the currently cued/loaded video. The final player state after this function executes will be `playing` (1).
  - Note: A playback only counts toward a video's official view count if it is initiated via a native play button in the player.

- `player.pauseVideo():Void`

  - Pauses the currently playing video. The final player state after this function executes will be `paused` (2) unless the player is in the `ended` (0) state when the function is called, in which case the player state will not change.

- `player.seekTo(seconds:Number):Void`

  - Seeks to a specified time in the video. If the player is paused when the function is called, it will remain paused. If the function is called from another state (`playing`, etc.), the player will play the video.

### Changing the player volume

- `player.mute():Void`
  
  - Mutes the player.

- `player.unMute():Void`

  - Unmutes the player.

- `player.isMuted():Boolean`

  - Returns true if the player is muted, false if not.

- `player.setVolume(volume:Number):Void`

  - Sets the volume. Accepts an integer between 0 and 100.

- `player.getVolume():Number`

  - Returns the player's current volume, an integer between 0 and 100. Note that getVolume() will return the volume even if the player is muted.

### Playback status

- `player.getPlayerState():Number`

  - Returns the state of the player. Possible values are:

  	- -1 – unstarted
  	- 0 – ended
  	- 1 – playing
  	- 2 – paused
  	- 3 – buffering
  	- 5 - cued

 - `player.getCurrentTime():Number`

   - Returns the elapsed time in seconds since the video started playing.

### Retrieving video information

- `player.getDuration():Number`

  - Returns the duration in seconds of the currently playing video. Note that `getDuration()` will return 0 until the video's metadata is loaded, which normally happens just after the video starts playing.

- `player.getVideoUrl():String`

  - Returns the livecap.tv URL for the currently loaded/playing video.

- `player.getVideoEmbedCode():String`

  - Returns the embed code for the currently loaded/playing video.

### Adding or removing an event listener

- `player.addEventListener(event:String, listener:String):Void`

  - Adds a listener function for the specified `event`. The Events section below identifies the different events that the player might fire. The listener is a string that specifies the function that will execute when the specified event fires.

- `player.removeEventListener(event:String, listener:String):Void`

  - Removes a listener function for the specified `event`. The listener is a string that identifies the function that will no longer execute when the specified event fires.

## Events

The API fires events to notify your application of changes to the embedded player. As noted in the previous section, you can subscribe to events by adding an event listener when constructing the LiveCap.Player object, and you can also use the addEventListener function.

The API will pass an event object as the sole argument to each of those functions. The event object has the following properties:

- The event's `target` identifies the video player that corresponds to the event.
- The event's `data` specifies a value relevant to the event. Note that the `onReady` event does not specify a data property.

The following list defines the events that the API fires:

### onReady

This event fires whenever a player has finished loading and is ready to begin receiving API calls. Your application should implement this function if you want to automatically execute certain operations, such as playing the video or displaying information about the video, as soon as the player is ready.

### onStateChange

This event fires whenever the player's state changes. The `data` property of the event object that the API passes to your event listener function will specify an integer that corresponds to the new player state. Possible values are:

- -1 – unstarted
- 0 – ended
- 1 – playing
- 2 – paused
- 3 – buffering
- 5 - cued

When the player first loads a video, it will broadcast an `unstarted` (-1) event. When a video is cued and ready to play, the player will broadcast a video `cued` (5) event. In your code, you can specify the integer values or you can use one of the following namespaced variables:

- LiveCap.PlayerState.ENDED
- LiveCap.PlayerState.PLAYING
- LiveCap.PlayerState.PAUSED
- LiveCap.PlayerState.BUFFERING
- LiveCap.PlayerState.CUED

### onError

This event fires if an error occurs in the player. The API will pass an event object to the event listener function. That object's data property will specify an integer that identifies the type of error that occurred.

## Autoplay and Scripted Playback

The HTML5 `<video>` element, in certain mobile browsers (such as Chrome and Safari), only allows playback to take place if it's initiated by a user interaction (such as tapping on the player). For more information please refer to [Apple's documentation](https://developer.apple.com/library/safari/#documentation/AudioVideo/Conceptual/Using_HTML5_Audio_Video/AudioandVideoTagBasics/AudioandVideoTagBasics.html)

Due to this restriction, functions and parameters such as `autoplay` and `playVideo()` won't work in all mobile environments.
