Image Link Extractor Scripts
This repository contains two JavaScript snippets designed to be run in your web browser's developer console. These scripts are useful for quickly extracting and cleaning image links from specific types of webpages, and then copying the list of links to your clipboard.

Table of Contents
Overview

How It Works

Usage Guide

The Scripts

Overview
This tool provides two JavaScript snippets tailored to different webpage structures. Each script is designed to extract and clean image links from a specific page layout, making it easy to grab high-resolution image URLs and copy them for other uses, such as batch downloading with a tool like IDM.

How It Works
The scripts differ in how they locate and process images on a webpage.

Script 1: For Product Thumbnails

Finds Images by Class: This script targets all images on the page that have specific, hard-coded CSS class attributes (e.g., .pdp-mod-common-image).

Cleans a Specific Substring: It looks for and removes a fixed part of the image URL, such as _120x120q80.jpg_.webp, to get a link to the main, higher-quality image.

Logs and Copies: The cleaned links are printed to the browser's console and automatically copied to your clipboard.

Script 2: For Product Details

Finds Images by Container: This more dynamic script first locates a specific section of the webpage using its CSS ID (#module_product_detail).

Uses a Dynamic Regex: It uses a regular expression to intelligently remove the size and quality parameters (e.g., _2200x2200q80.jpg_.webp) from the URL. This makes it adaptable to different image sizes and file extensions like .jpg or .png.

Logs and Copies: The cleaned links are printed to the console and automatically copied to your clipboard.

Usage Guide
Follow these steps to use either script in your browser's developer console:

Navigate to the Webpage: Go to the page where you want to extract the image links.

Open Developer Tools: Right-click anywhere on the page and select "Inspect." Then, navigate to the Console tab.

Copy & Paste the Code: Find the script you need below, copy the entire code block, and paste it into the console's input area.

Run the Script: Press Enter to execute the script. The cleaned links will be displayed in the console and automatically copied to your clipboard.

Download Images (with IDM):

Open IDM (Internet Download Manager).

Click "Task" on the top-left corner and select "Add batch download from clipboard".

In the window that appears, click "Check all," select "Main Download Queue," and click "Ok."

Finally, click the "Start the queue" button to download all the images.

Note on Functionality: This script only extracts and copies links. It cannot automatically download images due to browser security restrictions. User interaction is required for each download.

The Scripts
Script 1: For Product Thumbnails
This script is for pages where the image elements have hard-coded class attributes.

// This script targets image elements on the currently loaded webpage with specific class attributes.

// Select all img tags with specific classes for product thumbnails.
const imgElements = document.querySelectorAll('img.pdp-mod-common-image.item-gallery__thumbnail-image');

const cleanedSrcLinks = [];

// Iterate over each img element to extract and clean its src attribute.
imgElements.forEach(img => {
    let src = img.getAttribute('src');
    if (src) {
        // Define the specific substring to remove from the image URL.
        const substringToRemove = "_120x120q80.jpg_.webp";

        // Replace the substring if it exists to get the main image link.
        if (src.includes(substringToRemove)) {
            src = src.replace(substringToRemove, "");
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
    tempTextArea.value = linksToCopy;
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

Script 2: For Product Details
This script is more dynamic and works on pages where the images are contained within a specific element, regardless of their individual class attributes.

// This script is now dynamic, allowing you to specify the container for the images.
// This makes it adaptable to different pages on the same website with similar structures.

// The CSS selector for the image container is now hard-coded to 'module_product_detail'.
// This removes the need for a user prompt.
const selector = '#module_product_detail';

// Select the main container for the product description using the provided selector.
const container = document.querySelector(selector);

if (container) {
    // Find all <img> tags within the container.
    const imgElements = container.querySelectorAll('img');
    const cleanedSrcLinks = [];

    // Define a regular expression to find and remove the dynamic part of the URL,
    // like "_2200x2200q80.jpg_.webp" or similar variations.
    // The regex is now updated to handle both .jpg and .png file extensions.
    const regexToRemove = /_\d+x\d+q\d+\.(jpg|png)_\.webp/g;

    // Iterate over each img element to extract and clean its src attribute.
    imgElements.forEach(img => {
        let src = img.getAttribute('src');
        if (src) {
            // Use the regular expression to replace the matched substring with an empty string.
            // This makes the script dynamic and adaptable to different image sizes/qualities.
            const cleanedSrc = src.replace(regexToRemove, "");
            cleanedSrcLinks.push(cleanedSrc);
        }
    });

    // Log the cleaned links to the console for verification.
    console.log("Cleaned Image Links from Product Details:");
    if (cleanedSrcLinks.length > 0) {
        cleanedSrcLinks.forEach(link => console.log(link));

        // --- Feature: Copy links to clipboard ---
        const linksToCopy = cleanedSrcLinks.join('\n');
        const tempTextArea = document.createElement('textarea');
        tempTextArea.value = linksToCopy;
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

} else {
    console.log(`Could not find the '${selector}' container on this page.`);
}
