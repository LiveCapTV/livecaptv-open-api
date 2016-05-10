# Computing Offset in Twitch Player

The Flash version of Twitch Player has exposed two public methods for telling which moment the current video playback is at. Thus we can use these two methods to compute how much current playback is behind the live stream.

## Getting the player instance

As of now, the id of Twitch Player object is either `swfobject-0` or `swfobject-1`. Thus we can use raw Javascript API to get access to these objects:
	
    var player = document.getElementById("swfobject-0") || document.getElementById("swfobject-1");

## Getting current playback time and video duration

The `player` variable we get from above code snippet is a Flash object. We can use the following exposed methods to query video playback attributes directly:

    var current = player.getVideoTime();
    var duration = player.getDuration();

## Computing offset

After getting the attributes, the offset is easy to compute:

    var offset = current - duration;

## Exceptions

When some network error occurs, the `player.getDuration()` will return `0`. Under such circumstances, we recommend not to do a capture because the client has already failed to watch the live stream.