---
tags:
  - local
  - python
  - youtube
---

The goal of this python tool  is to download lists from Youtube and convert them into  `.wav` format.

This are the steps the tool will take

- Clean UI with a drag and drop field for link to a playlist
- A button bellow that filed called Convert
- The tool will then take the List name and download all the videos and convert them into `.wav`
- As it convert it will then download the files into the local downloads folder of the computer it's in



## 1. Create a new Folder In the python lib repo

Create a new folder following the name convention for this tool in the Tools Repo
![[Pasted image 20260613113313.png]]



## 2. Install ffmpeg in the local computer 

On Linux, so the simplest install is through your package manager.

### Ubuntu 

``` bash
sudo apt update

sudo apt install ffmpeg

ffmpeg -version

which ffmpeg
```


If which ffmpeg prints a path (e.g. /usr/bin/ffmpeg), the YouTube app should pass its check.



## 3. Use cursor AI to compile a new app based on initial sample project.


## 4. Plex Naming and Tag convention


Plex's scanner actually cares more about **embedded metadata tags** than the file names themselves. If your folders are perfect but your tags are blank, Plex will still mess up.

- **Album Artist:** This is the most critical tag. For compilation albums (like movie soundtracks or "Hits of the 90s"), set the Album Artist to `Various Artists`, while keeping the individual performers in the _Track Artist_ tag.
  
- **Album:** Must match exactly across all tracks in that album.
  
- **Track Artist:** The specific artist for that track.
  
- **Track Number:** Use simple numbers (`1`, `2`, `3`).
  
- **Disc Number:** For multi-disc sets (`1/2`, `2/2`).