# ArchivEye

## Introduction

- TODO: Explain what ArchivEye does / problems it solves / who uses it
- TODO: Screenshots / Gifs

## Installation

---

### Windows

### 1. Install Tesseract

- Download and install the latest version 5.3.1 from [uni-mannheim](https://digi.bib.uni-mannheim.de/tesseract/tesseract-ocr-w64-setup-5.3.1.20230401.exe)

### 2. Install GhostScript

- Go to [this page](https://github.com/ArtifexSoftware/ghostpdl-downloads/releases) and download and install according to your system platform

### 3. Tell ArchivEye the location of the above two

- Open up `.env` file and modify the path to the installed locations of the above two programs accordingly

---

### Mac

- TODO

---

### Linux

- Figure it out by yourself (Jokes, it's TODO)

---

## TODO

### Backend

- [x] Add indexing system
  - [x] Add progress feedback
- [x] Set index path to be at app path by default
- [x] Add search system
- [ ] Add threading for multiple workers to index a directory

### Frontend

- [x] DARK THEME MYSELF PLZZZZ! IT'S HURTING MY OWN EYES
  - [ ] Fix inconsistent dark mode
- [x] Setup Page: Index Folder & PDF Document Folder setter
  - [x] Receive backend's OCR progress and display it on a horizontal progress bar
  - [x] Cross out (1) button after selection, cross out (2) button after indexing starts
  - [x] Make both of buttons disabled after indexing starts
  - [x] Add relevant random wait phrases
  - [x] When OCR is completed, show an overlay with a button that proceeds to search page
  - [x] Check if index DB already exists, if so provide an option to go straight to search
  - [x] Add option to index more documents
- [x] Refactor out index path setting
- [x] Search Page: Initial Layout
  - [x] Update search result continuously
  - [x] Display on a results table (Fix partial state issue)
  - [x] Tooltip on hover of the pdf document name
  - [x] Implement view to the side
  - [x] Spike: PDF Viewer
  - [x] Pagination of search result display
  - [ ] Spike: Search result highlighting


### Meta

- [ ] Add setup instructions & Test if it works
- [ ] Test Electron packaging
  - [ ] Fix the shitty canvas bug
- [ ] Add initial tests to verify OCR and Img extraction are working correctly with sample PDF and images and texts

## Design

### Indexing System

- User select an empty directory to store index files
- Index Logic
  - For each PDF document
    - Generate a UUID
      - Append the "UUID to book path relation" to a master CSV
      - Create a temp folder "IMG_{UUID}" for containing all images from the Ghostscript PDF
      - Create a folder "{UUID}" for txt for each page from OCR'd images
      - Delete temp folder for images

- Search Logic
  - Parse index db file into mapping relations
  - When user enters a search term, look up all folders under the same directory as the index db file
  - For any found records, append into a result list

- Render logic
  - For a given PDF file path and a page number, display it to the frontend