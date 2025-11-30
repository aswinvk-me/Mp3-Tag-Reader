# LSB Image Steganography (C Project)

   

A complete implementation of **LSB (Least Significant Bit) Image Steganography** in C.
This project hides a **text file** inside a **24-bit BMP image** and can also extract it back.

---

## 📌 Features

* Hide `.txt` files inside `.bmp` images
* Extract hidden messages accurately
* Uses 1-bit LSB encoding
* Input validation & error handling
* Fully modular code structure
* Clean logs for each step

---

## 📂 Project Structure

```
/
├── main.c                   # Operation selection (encode/decode)
├── encode.c / encode.h      # Encoding logic
├── decode.c / decode.h      # Decoding logic
├── common.h                 # Magic string (#*)
├── types.h                  # Custom typedefs & enums
├── secret.txt               # Sample secret file
├── output.txt               # Example decoded output
├── stego.bmp                # Example encoded image
```

---

## 🧠 How It Works

### 🔒 Encoding Process

1. Validate file arguments
2. Open source BMP, secret `.txt`, and output BMP
3. Check BMP capacity
4. Copy BMP header (54 bytes)
5. Encode into image LSBs:

   * Magic string (`#*`)
   * Secret file extension size
   * Secret file extension
   * Secret file size
   * Secret file data
6. Copy remaining image bytes

### 🔓 Decoding Process

1. Open stego BMP
2. Skip the header
3. Verify the magic string
4. Decode:

   * Extension size
   * Extension
   * File size
   * File content
5. Write extracted file

---

## ⚙️ Building

Compile using GCC:

```bash
gcc main.c encode.c decode.c -o stego
```

---

## 🚀 Usage

### **Encoding**

```bash
./stego -e input.bmp secret.txt output.bmp
```

If output name is missing:

```
stego.bmp
```

### **Decoding**

```bash
./stego -d stego.bmp recovered.txt
```

If output name is missing:

```
output
```

---

## 📄 Example

If `secret.txt` contains:

```
My password is SECRET ;)
```

After decoding:

```
output.txt → "My password is SECRET ;)"
```

---

## ✔️ Requirements

* GCC or any C compiler
* 24-bit BMP image (uncompressed)
* Secret file must be `.txt`

---

## 🔧 Future Improvements

* Encryption before embedding
* Support for any file type (binary mode)
* PNG/JPEG steganography
* GUI version
* CLI progress bar

---



## 👤 Author

**Aswin Chandra M A**
