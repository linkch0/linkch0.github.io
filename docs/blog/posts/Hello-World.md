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

## Uploading images

!!! info "Workflow"

    1. Convert a png, jpg into webp file
    2. Rename the webp file with its md5 hash
    3. Upload the webp file to SM.MS by `picgo`

Installation:

1. Install [md5sha1sum](http://microbrew.org/tools/md5sha1sum/) and [webp](https://developers.google.com/speed/webp/) by homebrew

    - `brew install md5sha1sum webp` 
    
    - Calculate the MD5 checksum for one or more files:
    
         `md5sum path/to/file1 path/to/file2 ...`
    
    - Compress a WebP file with default settings (q = 75) to the [o]utput file:
    
         `cwebp path/to/image_file -o path/to/output.webp`
    
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
    
    # Check if the correct number of arguments is provided
    if [ "$#" -ne 1 ]; then
        echo "Usage: $0 <image_path>"
        exit 1
    fi
    
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
    webp_path="$im_dir/$im_name.webp"
    /opt/homebrew/bin/cwebp -q 80 "$1" -o "$webp_path"
    
    # Calculate the hash of WebP file
    hash_value=$(/opt/homebrew/bin/md5sum "$webp_path" | awk '{print $1}') # (1)!
    hash_path="$im_dir/$hash_value.webp"
    mv "$webp_path" "$hash_path"
    
    # Upload the WebP file using picgo
    /opt/homebrew/bin/picgo upload "$hash_path"
    rm "$1" "$hash_path"
    # echo "Conversion and upload successful!"
    ```
    
    1.  Print the fifth column (a.k.a. field) in a space-separated file:
        - `awk '{print $5}' path/to/file`
    

## Edit with Typora

1.   Set indent size to 4
2.   List
     -   Nested list
         -   Nested list
3.   Set image uploader to [custom command](#uploading-images)
