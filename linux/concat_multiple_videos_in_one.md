# Concat multiple videos in one

Create a file `files.txt` containing absolute or relative paths to the videos about to be merged
file 'file1.mp4'
file '/path/to/file2.mp4'
file 'file3.mp4'

Then execute following command:
`ffmpeg -f concat -safe 0 -i files.txt -c copy output.mp4`
