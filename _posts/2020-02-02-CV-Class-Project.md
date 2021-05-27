---

---
# Colorizing Russia
In this project I try to reconstruct a color photo from the black and white phots taken by the Russian photographer Sergey Prokudin-Gorsky back in the early 19s.

## Background
*From Wikipedia*  
Around 1905, Prokudin-Gorsky envisioned and formulated a plan to use the emerging technological advances that had been made in color photography to document the Russian Empire systematically. Through such an ambitious project, his ultimate goal was to educate the schoolchildren of Russia with his "optical color projections" of the vast and diverse history, culture, and modernization of the empire.

Outfitted with a specially equipped railroad-car darkroom provided by Tsar Nicholas II and in possession of two permits that granted him access to restricted areas and cooperation from the empire's bureaucracy, Prokudin-Gorsky documented the Russian Empire between around 1909 and 1915. He conducted many illustrated lectures of his work. His photographs offer a vivid portrait of a lost world—the Russian Empire on the eve of World War I and the coming Russian Revolution. His subjects ranged from the medieval churches and monasteries of old Russia, to the railroads and factories of an emerging industrial power, to the daily life and work of Russia's diverse population.

### The Tri-Filter Camera
*From Wikipedia*  
The method of color photography used by Prokudin-Gorsky was first suggested by James Clerk Maxwell in 1855 and demonstrated in 1861, but good results were not possible with the photographic materials available at that time. In imitation of the way a normal human eye senses color, the visible spectrum of colors was divided into three channels of information by capturing it in the form of three black-and-white photographs, one taken through a red filter, one through a green filter, and one through a blue filter. The resulting three photographs could be projected through filters of the same colors and exactly superimposed on a screen, synthesizing the original range of color additively.
The most common camera model during that time used a single oblong plate 9 cm wide by 24 cm high, the same format as Prokudin-Gorsky's surviving negatives, and it photographed the images in unconventional blue-green-red sequence, which is also a characteristic of Prokudin-Gorsky's negatives if the usual upside-down image in a camera and gravity-compliant downward shiftings of his plates are assumed.

## Colorizing Russia
In an effort to colorize these photos, I implemented simple image processing. 

### Splitting into RGB channels
The process starts with splitting the raw image in to three separate images representing the RGB channel. This procedure is pretty simple just vertically devided the raw image into three seperated images.

**The onion church in its original film format and seperated RGB images**
<!-- ![raw image](images/onion_church.png)
![bgr image](images/onion_church_rgb.png) -->
<div class="row">
  <div class="column">
	<img src="/assets/images/color_russia/onion_church.png" height="500px">
	<img src="/assets/images/color_russia/onion_church_rgb.png" height="300px">
  </div>
</div>

### Align Channels
Now here comes the crucial part of reconstructing a color image, since the seperated RGB images are not perfectyly aligned, meaning there are certain amounts of deviation between each channel.

#### Naive Approach
Here we can see that by blindly stacking the three channels together produces a weird photo with strange colors and shades.
![naive approach](/assets/images/color_russia/onion_church_naive.png)

### Using SSD or NCC to Align The Images
A much proper way to align the three channels is to use some metrics to determine what amount of deviation/shift we have to give to a certain channel for it to be better align with another. Some common metrics includes Sum of Squared Differences (SSD) and normalized cross-correlation (NCC).  
However for each channel image there are some borders along the sides which could influenced alignment by adding uncertainties to SSD or NCC. To avoid that I use center cropping to just check the alignment of the center portion of each channel. Then I grid search within a range of possible shifts for the red/green color channels relative to the blue channel. For single scale photos, I searched through shifts in the x and y directions of up to 50 pixels. For multiscale I first start with 1/16 of the image size and go down to 1/2 of the image size for the optimal shift.

<div class="row">
  <div class="column">
  	<figure>
	<img src="/assets/images/color_russia/cathedral_rgb_s.png"  height="200px">
    <figcaption>R[12, 3], G[5, 2]</figcaption>
	</figure>
  	<figure>
	<img src="/assets/images/color_russia/harvesters_rgb_s.png"  height="200px">
    <figcaption>R[128, 16], G[64, 16]</figcaption>
	</figure>
  	<figure>
    <img src="/assets/images/color_russia/icon_rgb_s.png" height="200px">
    <figcaption>R[96, 16], G[48, 16]</figcaption>
	</figure>
  </div>
  <div class="column">
  	<figure>
    <img src="/assets/images/color_russia/onion_church_rgb_s.png" height="200px">
    <figcaption>R[112, 32], G[48, 32]</figcaption>
	</figure>
  	<figure>
    <img src="/assets/images/color_russia/self_portrait_rgb_s.png" height="200px">
    <figcaption>R[176, 32], G[80, 32]</figcaption>
	</figure>
  	<figure>
    <img src="/assets/images/color_russia/three_generations_rgb_s.png" height="200px">
    <figcaption>R[112, 16], G[48, 16]</figcaption>
	</figure>
  </div>	
  <div class="column">
  	<figure>
    <img src="/assets/images/color_russia/girls_rgb_s.png" height="200px">
    <figcaption>R[0, 1], G[-1, 1]</figcaption>
	</figure>
  	<figure>
    <img src="/assets/images/color_russia/church_rgb_s.png" height="200px">
    <figcaption>R[13, -1], G[6, 0]</figcaption>
	</figure>
  	<figure>
    <img src="/assets/images/color_russia/melons_rgb_s.png" height="200px">
    <figcaption>R[192, 16], G[96, 16]</figcaption>
	</figure>
  </div>
  <div class='column'>
	<figure>
    <img src="/assets/images/color_russia/lady_rgb_s.png" height="200px">
    <figcaption>R[112, 16], G[48, 16]</figcaption>
	</figure>
  	<figure>
    <img src="/assets/images/color_russia/monastery_rgb_s.png" height="200px">
    <figcaption>R[3, 2], G[-3, 2]</figcaption>
	</figure>
  	<figure>
    <img src="/assets/images/color_russia/village_rgb_s.png" height="200px">
    <figcaption>R[144, 16], G[64, 16]</figcaption>
	</figure>
  </div>	
  <div class='column'>
  	<figure>
    <img src="/assets/images/color_russia/tobolsk_rgb_s.png" height="200px">
    <figcaption>R[7, 3], G[3, 3]</figcaption>
	</figure>
  	<figure>
    <img src="/assets/images/color_russia/workshop_rgb_s.png" height="200px">
    <figcaption>R[112, -16], G[48, 0]</figcaption>
	</figure>
  	<figure>
    <img src="/assets/images/color_russia/train_rgb_s.png" height="200px">
    <figcaption>R[80, 32], G[48, 0]</figcaption>
	</figure>
  </div>
</div>

### Problem - Emir
The standard code I use works with most of the images but with exceptions. The photo of the emir of Bukhara, due to different brightness of red and blue channel, the alignment algorithm produced a misaligned photo. My work around is to use the green channel as the reference channel and align the blue and red channel to it. Below we can see the difference of the two methods.
<figure>
<img src="/assets/images/color_russia/emir_rgb.png" height="300px">
<figcaption>align to blue channel</figcaption>
</figure>
<figure>
<img src="/assets/images/color_russia/emir_rgb_.png" height="300px">
<figcaption>align to green channel</figcaption>
</figure>
