---
layout: post
title: "ImageMagick, JPEGs, and Orientation, Oh My"
date: 2012-06-13 15:15
comments: true
categories: blog ruby rails code
---

I've been working on a new project and decided to use CarrierWave to handle image uploads (and minor automatic manipulation).  Everything looked great, but then my new boss, who has a penchant for finding the one or two things wrong with your latest well-tested feature uploaded a JPEG that looked fine in Preview, but automatically rotated on upload.

After checking through the directory, it seemed that only the processed images were getting rotated.  Actually, 'rotated' is a misnomer, they were actually just losing their orientation.  JPEGs have EXIF meta data that can contain the orientation of a picture, no matter how it's stored.  This allows cameras to store everything as a 640x480, but display some in the reverse (480x640).  The only thing different when the camera writes the image is what orientation the gyroscope adds to the meta data.

As it turns out, imagemagick was stripping out this data during conversion.  But lo and behold, there is a way around the problem.  Thank you <code>auto-orient</code> for being so awesome!

What I had before was this:

``` ruby
  version :wide do
    process :resize_to_fill => [270, 150]
  end

  version :small do
    process :resize_to_fill => [180, 180]
  end

  version :thumb do
    process :resize_and_pad => [90, 90]
  end

  version :tiny do
    process :resize_to_fill => [40, 40]
  end
```

I simply added this function, which added the 'auto_orient' call prior to format conversion:

``` ruby
  def convert_to_png
    manipulate! do |image|
      image.auto_orient
      image.format('png')
      image
    end
  end
```

And then called each of them in the versions

``` ruby
  version :wide do
    process :convert_to_png
    process :resize_to_fill => [270, 150]
  end

  version :small do
    process :convert_to_png
    process :resize_to_fill => [180, 180]
  end

  version :thumb do
    process :convert_to_png
    process :resize_and_pad => [90, 90]
  end

  version :tiny do
    process :convert_to_png
    process :resize_to_fill => [40, 40]
  end

  def convert_to_png
    manipulate! do |image|
      image.auto_orient
      image.format('png')
      image
    end
  end
```

Thank goodness for open source allowing me to read what was going on in MiniMagick's code :)
