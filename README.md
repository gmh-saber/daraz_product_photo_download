# 🖼️ Image Link Extractor Scripts

A guide to different browser console tools

![App Screenshot](https://github.com/gmh-saber/daraz_product_photo_download/blob/main/screencapture-gmh-saber-github-io-daraz-product-photo-download-2025-08-03-23_33_32.png)

🔗 **Web:** [gmh-saber.github.io/daraz_product_photo_download](https://gmh-saber.github.io/daraz_product_photo_download/)

---

---

## 📄 Overview

This project provides **two JavaScript snippets** designed to be run in the **browser's developer console**. Each script targets a different kind of product image structure and helps you extract cleaned image URLs, which are automatically copied to your clipboard.

### 🧠 How It Works

#### 🔹 Script 1: Product Thumbnails

1. **Targets by Class** – Searches for images with the class like `pdp-mod-common-image`.
2. **Cleans the URL** – Removes suffixes like `_120x120q80.jpg_.webp` to reveal the original.
3. **Copies to Clipboard** – Outputs cleaned links and copies them for easy use.

#### 🔹 Script 2: Product Details

1. **Targets by Container** – Focuses on the `#module_product_detail` element.
2. **Uses Regex** – Dynamically removes size/quality params from `.jpg` and `.png` URLs.
3. **Copies to Clipboard** – Extracted links are cleaned and auto-copied.

---

## 🚀 Usage Guide

### 🧭 Step-by-step

1. **Open the Target Webpage** – Visit the page with the product images.
2. **Open Developer Tools**  
   - **Chrome/Firefox/Edge:** Right-click → "Inspect" → Console tab  
   - **Safari:** Preferences → Advanced → Enable "Show Develop Menu" → Console
3. **Copy the Script** – Choose the appropriate script below and copy it.
4. **Paste and Run** – Paste into the console and press `Enter`.
5. **Download Images**  
   - Open **Internet Download Manager (IDM)**
   - Go to `Task > Add batch download from clipboard`
   - Select all, click OK → Start the queue

> ⚠️ **Note:** These scripts only extract and copy image URLs. They do not auto-download files due to browser restrictions.

---

## 💻 The Code

### 📜 Script 1 – Product Thumbnails

```javascript
// This script targets image elements on the currently loaded webpage with specific class attributes.

// Select all img tags with specific classes for product thumbnails.
const imgElements = document.querySelectorAll('img.pdp-mod-common-image.item-gallery__thumbnail-image');

const cleanedSrcLinks = [];

// Iterate over each img element to extract and clean its src attribute.
imgElements.forEach(img => {
    let src = img.getAttribute('src');
    if (src) {
        // Define a regular expression to match the dynamic substring.
        // This pattern looks for "_<width>x<height>q<quality>.<format>_.webp"
        // The (?:...) creates a non-capturing group for the file extension.
        // It matches .jpg, .jpeg, .png, .gif, .bmp, .svg, .webp (and others if needed)
        const substringPattern = /_\d+x\d+q\d+\.(?:jpg|jpeg|png|gif|bmp|svg|webp)_.webp/i;

        // Replace the matched pattern if it exists to get the main image link.
        if (substringPattern.test(src)) {
            src = src.replace(substringPattern, "");
        }
        cleanedSrcLinks.push(src);
    }
});

// Log the cleaned links to the console for verification.
console.log("Cleaned Image Source Links from Current Page:");
if (cleanedSrcLinks.length > 0) {
    cleanedSrcLinks.forEach(link => console.log(link));

    // --- Feature: Copy links to clipboard ---
    const linksToCopy = cleanedSrcLinks.join('\n');
    const tempTextArea = document.createElement('textarea');
    tempTextArea.value = linksToopy;
    tempTextArea.style.position = 'fixed';
    tempTextArea.style.left = '-9999px';
    document.body.appendChild(tempTextArea);
    tempTextArea.focus();
    tempTextArea.select();
    try {
        const successful = document.execCommand('copy');
        const msg = successful ? 'successfully' : 'unsuccessfully';
        console.log(`Links copied to clipboard ${msg}!`);
    } catch (err) {
        console.error('Oops, unable to copy links to clipboard:', err);
        console.log('You can manually copy the links from the console output above.');
    } finally {
        document.body.removeChild(tempTextArea);
    }

} else {
    console.log("No matching image links found with the specified pattern.");
}

````

---

### 📜 Script 2 – Product Details (Dynamic)

```javascript
// Dynamically targets detailed images and cleans URLs.
const selector = '#module_product_detail';
const container = document.querySelector(selector);

if (container) {
    const imgElements = container.querySelectorAll('img');
    const cleanedSrcLinks = [];
    const regexToRemove = /_\d+x\d+q\d+\.(jpg|png)_\.webp/g;

    imgElements.forEach(img => {
        let src = img.getAttribute('src');
        if (src) {
            const cleanedSrc = src.replace(regexToRemove, "");
            cleanedSrcLinks.push(cleanedSrc);
        }
    });

    console.log("Cleaned Image Links:");
    if (cleanedSrcLinks.length > 0) {
        cleanedSrcLinks.forEach(link => console.log(link));
        const linksToCopy = cleanedSrcLinks.join('\n');
        const tempTextArea = document.createElement('textarea');
        tempTextArea.value = linksToCopy;
        tempTextArea.style.position = 'fixed';
        tempTextArea.style.left = '-9999px';
        document.body.appendChild(tempTextArea);
        tempTextArea.select();
        document.execCommand('copy');
        document.body.removeChild(tempTextArea);
        console.log("Links copied to clipboard!");
    } else {
        console.log("No matching images found.");
    }
} else {
    console.log("Container not found:", selector);
}
```

---

## 🔧 Features

* ✅ Extracts high-quality image links
* ✅ Automatically copies them to your clipboard
* ✅ Works on both thumbnails and detailed product pages
* ❌ Does not download images automatically (browser limitation)

---

## 📂 Project Structure

```
📦 image-link-extractor/
├── README.md
├── script1-thumbnail.js
├── script2-details.js
└── index.html (optional demo)
```

---

## 📎 License

This project is licensed under the [MIT License](LICENSE).

---

> Created with ❤️ using JavaScript + TailwindCSS

> Let me know if you'd like it to include live screenshots, deploy links, or be broken into multiple Markdown files.
