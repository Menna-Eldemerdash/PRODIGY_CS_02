# PRODIGY_CS_02
This project demonstrates a simple encryption and decryption mechanism for images using Python's Pillow library. The encryption process shifts the pixel values of the image by a given key, and the decryption reverses this operation. Below is an explanation of how the code works step by step.

How It Works
1. Image Encryption
The encrypt_image function encrypts an image by modifying its RGB pixel values. Here's how:

Input:
input_image_path: Path to the input image.
output_image_path: Path where the encrypted image will be saved.
key: Encryption key to shift pixel values.
Process:
The image is opened using the Pillow library (Image.open).
Each pixel's RGB values are incremented by the encryption key and wrapped around using modulo 256 (% 256) to ensure the values remain within valid RGB range (0-255).
The modified image is saved to the specified output path.
Output: The encrypted image.
2. Image Decryption
The decrypt_image function decrypts an image by reversing the encryption process. Here's how:

Input:
input_image_path: Path to the encrypted image.
output_image_path: Path where the decrypted image will be saved.
key: Encryption key used during encryption.
Process:
The image is opened using Pillow.
Each pixel's RGB values are decremented by the encryption key and wrapped around using modulo 256 (% 256).
The modified image is saved to the specified output path.
Output: The decrypted image.
3. Displaying the Images
The show_images function visualizes the original, encrypted, and decrypted images side by side using Matplotlib:

Input: Three images (original, encrypted, decrypted).
Process: Uses Matplotlib's subplots to display all three images in a single row for easy comparison.
Output: A graphical display of the images.
Usage
Prerequisites
Install the required libraries:
bash
Copy code
pip install pillow matplotlib
Code Example
python
Copy code
key = 1000  # Encryption key
original_image_path = "bmw.jpg"
encrypted_image_path = "encrypted_image.jpg"
decrypted_image_path = "decrypted_image.jpg"

# Process images
original = Image.open(original_image_path)
encrypted = encrypt_image(original_image_path, encrypted_image_path, key)
decrypted = decrypt_image(encrypted_image_path, decrypted_image_path, key)

# Show images
show_images(original, encrypted, decrypted)
Function Breakdown
encrypt_image
Encrypts an image by shifting each pixel's RGB values.

python
Copy code
def encrypt_image(input_image_path, output_image_path, key):
    img = Image.open(input_image_path)
    pixels = img.load()

    for i in range(img.width):
        for j in range(img.height):
            r, g, b = pixels[i, j]
            pixels[i, j] = ((r + key) % 256, (g + key) % 256, (b + key) % 256)

    img.save(output_image_path)
    return img
decrypt_image
Decrypts an image by reversing the encryption process.

python
Copy code
def decrypt_image(input_image_path, output_image_path, key):
    img = Image.open(input_image_path)
    pixels = img.load()

    for i in range(img.width):
        for j in range(img.height):
            r, g, b = pixels[i, j]
            pixels[i, j] = ((r - key) % 256, (g - key) % 256, (b - key) % 256)

    img.save(output_image_path)
    return img
show_images
Displays the original, encrypted, and decrypted images.

python
Copy code
def show_images(original, encrypted, decrypted):
    fig, axs = plt.subplots(1, 3, figsize=(15, 5))

    axs[0].imshow(original)
    axs[0].set_title("Original Image")
    axs[0].axis("off")

    axs[1].imshow(encrypted)
    axs[1].set_title("Encrypted Image")
    axs[1].axis("off")

    axs[2].imshow(decrypted)
    axs[2].set_title("Decrypted Image")
    axs[2].axis("off")

    plt.tight_layout()
    plt.show()
Example Results
After running the script:

Original Image: Displays the unaltered image.
Encrypted Image: Shows the image with pixel values shifted, appearing scrambled.
Decrypted Image: The original image restored after reversing the encryption.
Note
The key must be the same for both encryption and decryption.
Using a very large key (e.g., 1000) will work due to the modulo operation ensuring values remain within range.
