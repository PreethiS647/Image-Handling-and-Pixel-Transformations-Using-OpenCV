# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** PREETHI S 
- **Register Number:** 212223230157

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```

import cv2
import numpy as np
import matplotlib.pyplot as plt
img =cv2.imread('Eagle_in_Flight.jpg',cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

```


#### 2. Print the image width, height & Channel.
```
img.shape

```

#### 3. Display the image using matplotlib imshow().
```
img_gray = cv2.cvtColor(img_rgb, cv2.COLOR_RGB2GRAY)
plt.imshow(img_gray,cmap='gray')
plt.show()

```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```

img=cv2.imread('Eagle_in_Flight.jpg')
cv2.imwrite('Eagle.png',img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```
img=cv2.imread('Eagle.png')
img_rgb = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)

```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```
plt.imshow(img)
plt.show()
img.shape

```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```
crop = img_rgb[0:450,200:550] 
plt.imshow(crop[:,:,::-1])
plt.title("Cropped Region")
plt.axis("off")
plt.show()
crop.shape

```

#### 8. Resize the image up by a factor of 2x.
```
res= cv2.resize(crop,(200*2, 200*2))

```

#### 9. Flip the cropped/resized image horizontally.
```
flip= cv2.flip(res,1)
plt.imshow(flip[:,:,::-1])
plt.title("Flipped Horizontally")
plt.axis("off")

```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```
img=cv2.imread('Apollo-11-launch.jpg',cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
img_rgb.shape

```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```
text = cv2.putText(img_rgb, "Apollo 11 Saturn V Launch, July 16, 1969", (300, 700),cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 255, 255), 2)  
plt.imshow(text, cmap='gray')  
plt.title("New image")
plt.show()  

```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```
rcol= (255, 0, 255)
cv2.rectangle(img_rgb, (400, 100), (800, 650), rcol, 3)  

```

#### 13. Display the final annotated image.
```
plt.title("Annotated image")
plt.imshow(img_rgb)
plt.show()

```

#### 14. Read the image ('Boy.jpg').
```
img =cv2.imread('boy.jpg',cv2.IMREAD_COLOR)
img_rgb= cv2.cvtColor(img, cv2.COLOR_BGR2RGB) 

```

#### 15. Adjust the brightness of the image.
```
m = np.ones(img_rgb.shape, dtype="uint8") * 50

```

#### 16. Create brighter and darker images.
```
img_brighter = cv2.add(img_rgb, m)  
img_darker = cv2.subtract(img_rgb, m)  

```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(img_rgb), plt.title("Original Image"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(img_brighter), plt.title("Brighter Image"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(img_darker), plt.title("Darker Image"), plt.axis("off")
plt.show()

```

#### 18. Modify the image contrast.
```
matrix1 = np.ones(img_rgb.shape, dtype="float32") * 1.1
matrix2 = np.ones(img_rgb.shape, dtype="float32") * 1.2
img_higher1 = cv2.multiply(img.astype("float32"), matrix1).clip(0,255).astype("uint8")
img_higher2 = cv2.multiply(img.astype("float32"), matrix2).clip(0,255).astype("uint8")

```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(img), plt.title("Original Image"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(img_higher1), plt.title("Higher Contrast (1.1x)"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(img_higher2), plt.title("Higher Contrast (1.2x)"), plt.axis("off")
plt.show()

```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```
b, g, r = cv2.split(img)
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(b, cmap='gray'), plt.title("Blue Channel"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(g, cmap='gray'), plt.title("Green Channel"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(r, cmap='gray'), plt.title("Red Channel"), plt.axis("off")
plt.show()

```

#### 21. Merged the R, G, B , displays along with the original image
```
merged_rgb = cv2.merge([r, g, b])
plt.figure(figsize=(5,5))
plt.imshow(merged_rgb)
plt.title("Merged RGB Image")
plt.axis("off")
plt.show()

```

#### 22. Split the image into the H, S, V components & Display the channels.
```
hsv_img = cv2.cvtColor(img, cv2.COLOR_RGB2HSV)
h, s, v = cv2.split(hsv_img)
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(h, cmap='gray'), plt.title("Hue Channel"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(s, cmap='gray'), plt.title("Saturation Channel"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(v, cmap='gray'), plt.title("Value Channel"), plt.axis("off")
plt.show()

```
#### 23. Merged the H, S, V, displays along with original image.
```
merged_hsv = cv2.cvtColor(cv2.merge([h, s, v]), cv2.COLOR_HSV2RGB)
combined = np.concatenate((img_rgb, merged_hsv), axis=1)
plt.figure(figsize=(10, 5))
plt.imshow(combined)
plt.title("Original Image  &  Merged HSV Image")
plt.axis("off")
plt.show()

```

## Output:
- ### **i)** Read and Display an Image.

 1.Read 'Eagle_in_Flight.jpg' as grayscale and display:
  
![420200105-8fbee7a1-6682-4ebc-bf5d-0e99168fe414](https://github.com/user-attachments/assets/96ccb0d6-0860-443a-8f51-81ff1defca86)


2.Save image as PNG and display:

![420200261-f3c7b81e-a1d3-47d8-8bce-41506c62019f](https://github.com/user-attachments/assets/81d21c86-2e6b-4824-ba06-0836ab82a72b)


3.Cropped image:

![420200519-6844ce30-4221-4a0f-baa4-ffb871f70048](https://github.com/user-attachments/assets/579801d7-1272-4d02-b559-6bb751e2b021)


4.Resize and flip Horizontally:

![420203051-52f120d2-1e32-4f45-8ca6-30b834ada0d1](https://github.com/user-attachments/assets/235fad2c-7706-436e-b7cb-d1e103f7a980)


5.Read 'Apollo-11-launch.jpg' and Display the final annotated image:

![420201640-f9f8af66-0811-4ef7-93dd-26fd825533b7](https://github.com/user-attachments/assets/82032425-4ff3-4649-b2e3-6d38bd4ace1c)

 
- ### **ii)** Adjust Image Brightness.
- 1.Create brighter and darker images and display:

![420755440-2fbdf2e6-53b6-4789-b1f7-1c04a2a58af0](https://github.com/user-attachments/assets/8f56fd95-80b8-4ee1-9b69-d4365bc6c63e)


 ![420757888-84944e6d-1f8a-4db8-8f53-d3d2bbbd6e1c](https://github.com/user-attachments/assets/b021e4ea-9745-4272-bb1b-b26374733569)


![420757924-217de5b6-93f7-4495-95a6-549a1a182976](https://github.com/user-attachments/assets/8ee64fcf-ac4e-476d-b243-190c1fd8141f)

  
-  ### **iii)** Modify Image Contrast.

1. Modify contrast using scaling factors 1.1 and 1.2:

![420758318-4139717b-33aa-43b6-9bc2-5783780a1eb5](https://github.com/user-attachments/assets/7fd60d94-79da-40b3-be19-62f3b68e92fc)


![420758360-c96ec7ac-58aa-4729-9431-fdf31838a5f7](https://github.com/user-attachments/assets/8159e66a-6fb2-49e8-8de2-5ee196762da0)


![420758386-e19b467e-0ab4-44af-a235-921af100fe3d](https://github.com/user-attachments/assets/cf3760dc-659e-475c-a5ef-f7c1f130fb99)


- ### **iv)** Generate Third Image Using Bitwise Operations.

1.Split 'Boy.jpg' into B, G, R components and display:

![420755162-30364c56-0f70-4d05-b1fe-e504bbc830f4](https://github.com/user-attachments/assets/9e406189-ca97-4fe5-a92f-a097f7d6a67b)


![420755185-fc200792-bf96-4e55-bb12-d9c07df40092](https://github.com/user-attachments/assets/908a8c90-e762-47da-89f0-69b600a0e817)


![420755209-86c9a27b-a0ac-4cdd-924b-bd3173a3cee9](https://github.com/user-attachments/assets/f894973a-0be1-4aa3-b744-a8a2ad18e0a6)

2.Merge the R, G, B channels and display:

![420202108-09d5507f-ae48-4ab3-bc7d-9b7466ce7e81](https://github.com/user-attachments/assets/18e5301a-cba2-4fdc-8011-3962167b27e5)

3.Split the image into H, S, V components and display:

![420758632-5cfbee49-3082-44da-ab63-fbe813392013](https://github.com/user-attachments/assets/7127b5a0-162a-42ce-be13-beef27eacf19)

![420766585-74412dc1-b2a1-4261-af9c-0bec8f2165d6](https://github.com/user-attachments/assets/d988a296-59ee-4ac9-8602-7d46ff7ada09)

![420766607-c0612cd0-1dcc-4c4f-b9f7-501b18468184](https://github.com/user-attachments/assets/18b4c15f-ebb4-40a3-aeaf-d978b90fdb91)


4.Merge the H, S, V channels and display:

![420202189-3c8fa07d-31ff-4b14-87c1-061ffef0447e](https://github.com/user-attachments/assets/ae0ff7d9-3ec0-4bef-a7f8-70e5ac1cc15e)




## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.
