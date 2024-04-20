# my-work
hi i am going to take you step by step on how to run any project in this repo 

## running RTSP on HTTP pages 
* you need to get RTSP URL
* use ffmpeg to convert RTSP(real time streaming protocol) to HLS (HTTP live streaming)
## dependencies 
* use Choco or any tool to get the needed packages for the termenal
  use this code if you have choco
  ```choco install ffmpeg-full```
  or go to ffmpeg website (https://ffmpeg.org/)
* i used xampp to host my webpage
  ## how to start 
* after ffmpeg use this code to start generating the stream file the extension will be .m3u8 format
  like this ``ffmpeg -v verbose  -i rtsp://admin:12345678,@10.5.50.2:554/cam/realmonitor?channel=1 -vf scale=1920:1080  -vcodec libx264 -r 25 -b:v 1000000 -crf 31 -acodec aac  -sc_threshold 0 -f hls  -hls_time 5  -segment_time 5 -hls_list_size 5 any-folder\stream.m3u8``
  * -v verbose: it means be quiet
  * -i : for input
  * now enter your rtsp url
  * -vf : is the video format (scale=xxx)
  * the codec(vcodec) is x264
  * -r :is for the frame rate
  * -b:v is for the bit rate for the video(1000000)
  * -acodec aac : is the audio codec
  * -f hls : here i chose hls for my format
  * -hls_time 5: this is the default time
  * -segment_time 5: this is the default segment time
  * -hls_list_size 5 : this will how many packet will be available to watch more size mean more delay
  * and last the path that you want to store the stream files in it is crucial that you choose an isolated folder more details will be in the note down below
## how to stream it to http 
you can use html video tag like this ``<video id='myVideo'  class="video-js vjs-default-skin" width="400" height="300" controls>
		<source type="application/x-mpegURL" src="stream.m3u8" />
	</video>``
 the important thing is the ``src="stream.m3u8"`` you are going to get this file locally and stream it using the video tag 


## NOTE 
this method could be havy on the server one solution i thought about is to automate a process to delete any file with the extension *.ts*
that has been created for over some period of time 