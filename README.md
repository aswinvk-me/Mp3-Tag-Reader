# MP3 Tag Reader & Editor (ID3v2.3)

A command-line MP3 metadata **viewer and editor** built in C. This tool reads and modifies ID3v2.3 tags such as **Title, Artist, Album, Year, Content, and Comment**.

---

## 📌 Features

* View MP3 metadata (ID3v2.3)
* Edit individual tags
* Validate file format before processing
* Proper endian conversion while reading sizes
* Safe editing using temporary file mechanism
* Easy CLI usage with clear help menu

---

## 🗂️ Project Structure

```
/
├── main.c           # Entry point, handles CLI options
├── help_mp3.c       # Prints help menu
├── mp3_view.c       # Reads and displays MP3 metadata
├── mp3_edit.c       # Edits MP3 metadata
├── mp3_header.h     # Common includes & function prototypes
├── sample.mp3       # Sample MP3 file
```

---

## 🧠 How It Works

### 🔍 Viewing Tags (`-v`)

The program:

1. Opens the MP3 file
2. Checks for header signature `ID3` (ID3v2.3)
3. Skips header bytes
4. Reads the following frames:

   * `TIT2` → Title
   * `TPE1` → Artist
   * `TALB` → Album
   * `TYER` → Year
   * `TCON` → Content
   * `COMM` → Comment
5. Converts frame size from little-endian to big-endian
6. Prints metadata in a clean format

### ✏️ Editing Tags (`-e`)

1. Opens the original MP3 file and creates a temporary file
2. Searches for the specified tag (`-a`, `-t`, `-A`, `-y`, `-C`, `-c`)
3. Converts the new content size to the correct endian format
4. Writes updated tag to the temp file
5. Copies remaining bytes
6. Replaces the original file with the edited version

---

## 🚀 Usage

### ✔ View Tags

```
./a.out -v file.mp3
```

### ✔ Edit Tags

```
./a.out -e file.mp3 -[a t A y C c] "new_content"
```

### ✔ Help Menu

```
./a.out --help
```

---

## 🏷️ Tag Options

| Option | Tag  | Meaning                        |
| ------ | ---- | ------------------------------ |
| `-a`   | TPE1 | Artist Name                    |
| `-t`   | TIT2 | Song Title                     |
| `-A`   | TALB | Album Name                     |
| `-y`   | TYER | Release Year (1800–2100 check) |
| `-C`   | TCON | Content Type                   |
| `-c`   | COMM | Comment                        |

---

## 📄 Example

### View

```
./a.out -v sample.mp3
```

### Edit Title

```
./a.out -e sample.mp3 -t "My New Title"
```

### Edit Year

```
./a.out -e sample.mp3 -y "2019"
```

---

## ⚙️ Build Instructions

Compile using GCC:

```
gcc main.c help_mp3.c mp3_view.c mp3_edit.c -o mp3_tag_editor
```

---

## 📝 Notes

* Only supports **ID3v2.3** (most common standard)
* Editing year validates numeric range
* Uses safe endian conversion for size fields
* Does not parse extended headers or unsynchronized data

---

## 👤 Author

**Aswin Chandra M A**
