[![badge](https://img.shields.io/twitter/follow/api_video?style=social)](https://twitter.com/intent/follow?screen_name=api_video)

[![badge](https://img.shields.io/github/stars/apivideo/chyronavideo?style=social)](https://github.com/apivideo/chyronavideo)

[![badge](https://img.shields.io/discourse/topics?server=https%3A%2F%2Fcommunity.api.video)](https://community.api.video)

![](https://github.com/apivideo/API_OAS_file/blob/master/apivideo_banner.png)

<h1 align="center">api.video Chyron a video</h1>

[api.video](https://api.video) is the video infrastructure for product builders. Lightning fast video APIs for integrating, scaling, and managing on-demand & low latency live streaming features in your app.


# chyronavideo

A fork of record a video (description below)

The additional usage allows you to add a watermark and text to the video being uploaded to api.video.  This version fork does not offer a live stream option.

## Updated November 2021 with progressive upload. This feature allows for video upload while still recording, making the process easier and faster for your users.

# recordavideo

## record a video

There are 2 options:  Record & share & GO LIVE


### record and share

this will record your screen & camera.  when you stop your recording, it will upload the video to api.video, and give you a "share" url that you can share to anyone you want to see the video

## GO LIVE

This setting will livestream to the RTMP url saved in the index.js.  IT is set to a live stream at api.video.

## How does it work?

### GetUserMedia

The getUserMedia API will select your microphone, screen and camera. The video displays weill be placed on the screen, and then merged into a Canvas (based on the screen layout choice).  No audio is used in the video displays to avoid really loud and annoying feedback.  Trust me, you don't want to add audio to the video tags.

The canvas is read 60x/s and fed into a stream.  We append the audio to this stream - so it is connected to the final video. This stream is either recorded or streamed (based on users selection).

### Captions

the web speech api only works in chrome and Edge:
https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API
but it is pretty cool - real time captioning of your video - and then applied to the canvas (and saved to the recording).


### Uploading

We use api.video delegated tokens  to uplad the video (JS basically copied from https://upload.a.video)

### Streaming

There is a NodeJS server that accepts the socket from the webpage.  This server uses FFMPEG to convert the webRTC mediaRecrding from the browser canvas into RTMP.  Then the RTMP is fed to the api.video RTMP endpoint.

### use your own!

Copy this repo- and simply change the RTMP (the streaming URL), live (the player url for your livestream) and delegated token (for upload) variables at the top of the index.js.

