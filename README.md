# 🖼️ Image Link Extractor Scripts

A guide to different browser console tools

![App Screenshot](https://github.com/gmh-saber/daraz_product_photo_download/raw/main/assets/screencapture.png)

🔗 **Live Demo:** [gmh-saber.github.io/daraz_product_photo_download](https://gmh-saber.github.io/daraz_product_photo_download/)

---

## 📄 Overview

This page provides two JavaScript snippets designed to be run in your web browser's developer console. Each script is tailored to extract and clean image links from a specific type of webpage, and then copies the resulting links to your clipboard for easy use.

---

## 🧠 How It Works

### Script 1: For Product Thumbnails

1. **Finds Images by Class**  
   This script searches for all images on the page that have specific, hard-coded CSS class attributes (e.g., `pdp-mod-common-image`).

2. **Cleans a Specific Substring**  
   It then looks for a fixed part of the image URL, like `_120x120q80.jpg_.webp`, and removes it to give you a link to the main, higher-quality image.

3. **Logs and Copies**  
   All the cleaned links are logged to the console and automatically copied to your clipboard.

---

### Script 2: For Product Details

1. **Finds Images by Container**  
   This more dynamic script first locates a specific section of the webpage using the CSS ID `#module_product_detail` to focus on the product image gallery.

2. **Uses a Dynamic Regex**  
   It uses a regular expression to intelligently remove the size and quality parameters (e.g., `_2200x2200q80.jpg_.webp`) from the URL. This makes it adaptable to different image sizes and file extensions like `.jpg` or `.png`.

3. **Logs and Copies**  
   All the cleaned links are logged to the console and automatically copied to your clipboard.

---

## 🚀 Try It Live

> Click to preview the interactive tabbed version  
👉 [https://gmh-saber.github.io/daraz_product_photo_download](https://gmh-saber.github.io/daraz_product_photo_download)

---

## 📎 License

Licensed under the [MIT License](LICENSE)

---

> Built with ❤️ using JavaScript & TailwindCSS
