MEDIA FILES
Put these files in this folder with exactly these names (lowercase).
Any file that is missing is skipped automatically and the page shows a
line drawing in its place, so you can upload media whenever it is ready.

File                   Used on                              What it is
so101-teleop.mp4       so101.html, top                      Teleoperating the SO-101
so101-teleop.jpg       so101.html poster + home page tile   A clear mid-video frame
rover-tracking.mp4     rover.html, top                      YOLO26 + PID steering
rover-tracking.jpg     rover.html poster + home page tile   A frame with the target in view
rover-voice.mp4        rover.html, middle                   Conversational agent, keep the sound
rover-voice.jpg        rover.html poster                    A frame from that video
lidar-rviz.mp4         slam.html, middle                    RViz2 LiDAR clip (labeled as a placeholder)
lidar-rviz.jpg         slam.html poster                     A frame from that clip
sonar-raw.jpg          sonar.html, top + home page tile     Raw imaging-sonar frame
sonar-detections.jpg   sonar.html, middle (optional)        Detections after processing
forterra-telemetry.jpg forterra.html, top + home page tile  Telemetry screenshot
forterra-move-menu.jpg forterra.html, middle                Dropdown move menu screenshot
sonar-tile.jpg         home page sonar tile                 Top of the detections figure, cropped to fit
lukas.jpg              home page photo card + about.html    Portrait of you (vertical, head and shoulders)

Targets
- Videos: MP4 (H.264), 720p, under 8 MB if possible. GitHub's browser upload
  limit is 25 MB per file.
- Images: JPEG, about 1280 x 720, under 300 KB.
- KBR footage only with written approval.

Preparing files with ffmpeg on Windows (PowerShell)
  winget install Gyan.FFmpeg        (then open a new PowerShell window)

  Video without sound (teleop, tracking, LiDAR):
  ffmpeg -i "IN.mp4" -vf "scale=-2:720" -c:v libx264 -preset slow -crf 27 -pix_fmt yuv420p -movflags +faststart -an so101-teleop.mp4

  Video with sound (the voice demo):
  ffmpeg -i "IN.mp4" -vf "scale=-2:720" -c:v libx264 -preset slow -crf 27 -pix_fmt yuv420p -movflags +faststart -c:a aac -b:a 96k rover-voice.mp4

  Trim while converting: add  -ss 3 -to 40  right after the input file (start and end in seconds).

  Poster frame (5 seconds in; change 5 to pick a better moment):
  ffmpeg -ss 5 -i so101-teleop.mp4 -frames:v 1 -q:v 3 so101-teleop.jpg

Without ffmpeg
- Clipchamp (built into Windows 11): import, trim, Export at 720p.
- Poster frames: pause the video on a good frame, press Win+Shift+S, save
  the snip, then compress it at https://squoosh.app (MozJPEG, quality 75,
  resize width 1280).
