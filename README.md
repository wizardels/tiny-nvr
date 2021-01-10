FORK of https://github.com/hpaolini/tiny-nvr

To support ARM based systems (hopefully this will be merged in at some point)

```
docker run \
       -v $(pwd):/usr/data/recordings \
       -e TZ=America/Chicago \
       wizardels/tiny-nvr \
       rtsp://username:password@address:port//Streaming/Channels/2 \
       my_camera
```

With the default settings, the container creates a folder in the current directory (in the example the folder is named "my\_camera"), saves the stream in 15 minute segments,[^1] and initiates a daily cron job to delete recordings older than 3 days.

I added the following environment variables for additional customization. (Remember, environment variables are changed using the `-e` flag.)


| ENV                | Default       | Description |
| :----------------- | :----         | :------ |
| TZ                 | _Europe/Rome_ | timezone data |
| DIR_NAME_FORCE     | _false_       | use the folder name you pass as parameter during `docker run` even if it exists, otherwise it generates a new folder name |
| HOUSEKEEP_ENABLED  | _true_        | cron job to delete old recordings |
| HOUSEKEEP_DAYS     | _3_           | delete files older than this number of days, if HOUSEKEEP_ENABLED is enabled|
| VIDEO_SEGMENT_TIME | _900_         | seconds of each recording[^1] |
| VIDEO_FORMAT       | _mp4_           | save output as MKV or MP4 file |
