### Rewrite orientation and remove all metadata from all images in a directory.
mogrify -auto-orient -strip *

### Convert all images in directory to png or other format and provide output path.
mogrify -path output-path/ -format png *

### Convert markdown to odt
pandoc -t odt filename.md -o filename.odt

### Check free disk space
df

### Create new file
touch filename

### Download best quality audio from youtube
yt-dlp -f "bestaudio/best" -ciw -o "%(title)s.%(ext)s" -v --extract-audio

### Resize all images down to min 1000px horizontal size and max png compression (lossless)
mogrify -path path/ -resize 1000 -define png:compression-level=9 *.png

### Shell script to convert music files to opus without losing much quality
#!/bin/bashx
for file in *.{mp3,m4a,webm}; do
    if [ -f "$file" ]; then
        filename=$(basename "$file")
        output_file="${filename%.*}.opus"
        ffmpeg -i "$file" -c:a libopus -b:a 256k -map_metadata 0 -vbr on -compression_level 10 -y "$output_file"
    fi
done
