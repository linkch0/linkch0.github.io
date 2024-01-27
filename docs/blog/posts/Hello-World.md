---
date: 2023-12-30
slug: hello-world
authors: [linkchen]
categories: [Misc]
tags: [Updating]
comments: true
draft: true
---

# Hello world

Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.

<!-- more -->

## Metadata

```yaml linenums="1"
date: 2023-12-30
slug: hello-world
authors: [linkchen]
categories: [Misc]
tags: [Updating]
comments: true
draft: true
```

## Summary delimiter

In Markdown, `<!-- more -->` is a common "excerpt" or "summary" delimiter used by certain platforms or static site generators to indicate where a post or article should be truncated when displayed in a list or index.

## Uploading images by custom command

!!! info "Workflow"

    1. Convert a png, jpg into webp format by `cwebp`
    2. Add a watermark at bottom-right corner of the webp by `magick`
    3. Rename the webp with its md5 hash by `md5sum`
    4. Upload the webp file to SM.MS by `picgo`

Installation:

1. Install [md5sha1sum](http://microbrew.org/tools/md5sha1sum/), [WebP](https://developers.google.com/speed/webp/), and [ImageMagick](https://imagemagick.org/)  by homebrew

    - `brew install md5sha1sum webp imagemagick ` 

    - Calculate the MD5 checksum for one or more files:

         `md5sum path/to/file1 path/to/file2 ...`

    - Compress a WebP file with default settings (q = 75) to the [o]utput file:

         `cwebp path/to/image_file -o path/to/output.webp`

    -   Add your own watermark at bottom-right corner:

        `magick path/to/input.webp -pointsize 30 -fill white -gravity SouthEast -annotate +10+10 'your watermark' path/to/output.webp`

2. Install [Picgo-Core](https://github.com/PicGo/PicGo-Core)

    - `npm install picgo -g`

    - Upload an image from a specific path:

      `picgo upload path/to/image`

3. Register SM.MS [https://sm.ms/](https://sm.ms/) or [https://smms.app/](https://smms.app/)
    - Generate a secret token in SM.MS

    - Interactively select SM.MS hosting service:

      `picgo set uploader`

4. Write a bash script: `./upload.sh image.jpg`

    ```bash linenums="1" title="upload.sh"
    #!/bin/bash
    source ~/.bash_profile
    
    # Function to check if multiple commands exist
    commands_exist() {
      for cmd in "$@"; do
        if ! command -v "$cmd" >/dev/null 2>&1; then
          return 1  # Return non-zero if any command is not found
        fi
      done
      return 0  # Return zero if all commands are found
    }
    
    # Check if all command exists
    if ! commands_exist "cwebp" "magick" "md5sum" "picgo"; then
        echo "Error: Some commands are missing. Please install the required tools."
        exit 1
    fi
    
    upload_single(){
        # Check if the file exists
        if [ ! -f "$1" ]; then
            echo "Error: File not found: $1"
            exit 1
        fi
    
        # Get directory and name without extension
        im_dir=$(dirname "$1")
        im_name=$(basename "$1")
        im_name=${im_name%.*}
    
        # Convert the image to WebP using cwebp
        webp_path="$im_dir/${im_name}.webp"
        mark_path="$im_dir/${im_name}_mark.webp"
        cwebp -q 80 "$1" -o "$webp_path"
    
        # Add your own watermark to WebP
        watermark='© linkch0.github.io'
        magick "$webp_path" -pointsize 30 -fill white \
            -gravity SouthEast \
            -annotate +10+10 "$watermark" \
            "$mark_path"
    
        # Calculate the hash of WebP file
        hash_value=$(md5sum "$mark_path" | awk '{print $1}') # (1)!
        hash_path="$im_dir/${hash_value}.webp"
        mv "$mark_path" "$hash_path"
    
        # Upload the WebP file using picgo
        picgo upload "$hash_path"
        # upload_output=$(picgo upload "$hash_path" 2>&1)
        if ! [ $? -eq 0 ]; then
            echo "Error: Picgo upload failed."
            # echo $upload_output
            exit 1
        fi
        rm "$webp_path"
        mv "$hash_path" /Users/link/Pictures/Other/Picgo-Backup
        # echo "Conversion and upload successful!"
    }
    
    # Display the number of arguments
    # echo "Number of arguments: $#"
    args=("$@")
    # Upload all arguments using the array
    for arg in "${args[@]}"; do
        upload_single "$arg"
    done
    ```

    1.  Print the fifth column (a.k.a. field) in a space-separated file:
        - `awk '{print $5}' path/to/file`

5.   Here are the test image, watermark is at bottom-right corner:

     <figure markdown>
       ![Dummy Image](https://s2.loli.net/2024/01/11/FOm2DB3ng6EyTaP.webp)
       <figcaption>[https://dummyimage.com/1920x1080/](https://dummyimage.com/1920x1080/)</figcaption>
     </figure>

## Edit with Typora

1.   Set indent size to 4
2.   List
     -   Nested list
         -   Nested list
3.   Set image uploader to [custom command](#uploading-images)
