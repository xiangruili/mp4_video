# mp4_video
[![View mp4_video on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://www.mathworks.com/matlabcentral/fileexchange/74763-mp4_video)

Create mp4 video from figure window, like what Matalb VideoWriter does.

mp4_video is a subclass of VideoWriter, with following additional features:

1. The rect feature allows all OS to capture part of the figure, or to exclude UI control if needed.

2. The major benefit is to enable Linux support for mp4 format, using ffmpeg. If ffmpeg is not available, the uncompressed avi file will be kept.

3. Automatically use getframe() or print() to work for Matlab with remote connection.

 The usage is shown by this simple example for a moving circle:
 
     h = rectangle('Position', [0 0 1 1], 'Curvature', 1, 'FaceColor', 'k');
     axis equal; axis off; xlim([0 10]); ylim([0 10]); % set axis range
     vw = mp4_video('movingCircle.mp4', 4); % 4 frames per second
     for x = 0:9 % circle location range
         h.Position(1:2) = x; % move along diagonal
         vw.addFrame(); % add current frame to video buffer
     end
     vw.save(); % finish the video
