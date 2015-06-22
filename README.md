# makeqctoolsreport

This script accepts one or many video inputs and makes sidecar qctools reports for each.

# by the way
Here's an example of how to pipe video into ffprobe to make a qctools report while doing a transcode.
```
mkfifo temp1 ; ffmpeg -y -i inputvideo someoutput.mp4 -c:v rawvideo -c:a pcm_s24le -f nut temp1 | ffprobe -loglevel error -f lavfi "movie=temp1:s=v+a[in0][in1],[in0]signalstats=stat=tout+vrep+brng,cropdetect=reset=1,split[a][b];[a]field=top[a1];[b]field=bottom[b1],[a1][b1]psnr[out0];[in1]ebur128=metadata=1[out1]" -show_frames -show_versions -of xml=x=1:q=1 -noprivate | gzip > EXAMPLE.mov.qctools.xml.gz
```
