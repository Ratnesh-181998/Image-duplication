
Image Duplication:

Business Requirement:  

GeM mandates every product to have at least 3 different images of a product, to help buyer understand 
what one is procuring / paying for. This helps to cover all physical aspect of the entire product. 
However, majority of the sellers circumvent the system by uploading the same images over and over with 
minor modification. This undermines the purpose of the policy implemented. 
A sanitized marketplace has a good representation of the product, and the product image is the most 
important component to do so. 
To maintain the quality of the marketplace GeM wants to identify, prevent and remove the product 
catalogues with duplicate images. 
• GeM intends to give an alert in future to the sellers at the time of uploading the images if they 
are duplicate. 
• Gem wants to identify which product have duplicate images currently in system and remove 
duplicate images of the product. 

Proposed solution: 

The proposed solution is a system to automatically detect and prevent the upload of duplicate product 
images on the GeM platform. This system will: 
• Analyse the images uploaded by sellers. 
• Identify duplicate images. 
The objective of the Image Duplication model is to identify the duplicated images from the seller’s 
uploaded images based on: 
• Using an uploaded image as a base and checking the rest uploaded images for duplication. 
The solution will involve building a machine learning model capable of detecting duplicate images. This 
model will compare the images using difpy, a python library which is used for detecting duplicate 
images. 

Solution Consumption: 

Following are the stakeholders and processes where this solution can have impact: 
• Stakeholders – There are three stakeholders in the process:  
• Buyers: The buyer visits the marketplace to select the product of interest to add it to the cart and 
initiate the procurement process. The misrepresentation of the physical appearance of the 
product can misguide the buyer while selecting it.
• Sellers: The sellers upload images and manage their catalogues in CMS and the same is reflected 
in the marketplace. Due to sellers’ s lack of awareness about GeM norms regarding image upload 
that is to upload 3 different images of the product from different angles such as front, back, top, 
side, back, interior, close-ups or to show off the technology or science behind the product; sellers 
upload duplicate images of product. Duplicate images might hamper the chances of creating a 
good presentation of the product and hence can lead to low sales.  
• GEM SPV: Duplicate images can undermine market sanitization and the quality of the 
marketplace.

![Duplicate images can undermine market sanitization ](https://github.com/user-attachments/assets/f7aacabb-02b2-4dbc-9596-abcfff9b55e7)


Data: 

Images used are the product images available on GeM website. The required data can be fetched from 
the tables below: 
• Table: inb_variants  
• Table: inb_images 

Model Methodology:  

The code provided aims to automate the process of fetching, processing, and analysing product images 
for potential duplicates. The methodology involves several steps to extract relevant data from a MySQL 
database, process image URLs, download images, detect duplicates, and store the results for further 
analysis. 

Below is the methodology: 

1. Data Extraction: 
• The process starts with extracting relevant data from the gem_staging database. Specifically, it 
fetches product variants, their associated images, and related metadata based on specific 
category IDs. 
• A structured SQL query is executed to retrieve only active variants, ensuring the data is relevant 
and up to date. 
2. Data Processing: 
• The extracted data is processed to correct image URLs based on specific patterns. This ensures 
that all images are fetched from the correct server locations.

• Image URLs are adjusted to reflect the standard image format and path, which is necessary for 
consistent processing and storage. 
3. Image Download and Storage: 
• For each product variant, all associated images are downloaded and saved in a uniquely 
generated folder. This ensures that images from different categories or variants do not overlap. 
• The folder naming convention eliminates any special characters that could cause issues in file 
path resolution. 
4. Duplicate Image Detection: 
• The downloaded images are analysed for duplicates using the difPy library. This is done by 
comparing the images at a specified pixel size to identify those that are visually identical or 
similar. 
• The lower-quality duplicates are identified and listed, allowing for the retention of only the 
highest-quality images. 
5. Data Storage and Reporting: 
• If duplicates are detected, the information is stored in a CSV file, detailing the duplicate images 
and their associated product URLs. This file is organized by category ID, making it easier to trace 
back to the original product data. 
• All images, whether duplicates or not, are moved to a final directory specific to each category. 
This allows for easy access and future reference.

![flow of processes in this solution](https://github.com/user-attachments/assets/9beff5c0-7748-4c4a-a5ee-2aac352ed7d2)

Steps In Model:  
1. Extract Data from Database: 
• Execute SQL queries to extract product variant and image data for each category ID. 
• Store the extracted data in CSV files named after the respective category IDs. 
2. Process Image URLs: 
• Filter the Data Frame for relevant image URLs.
• Correct the image URLs to point to the appropriate server paths. 
• Ensure all URLs conform to a standard format for easier processing. 
3. Generate and Manage Folders: 
• Generate unique folder names using UUIDs to prevent conflicts. 
• Create directories to store downloaded images for each category and variant. 
4. Download Images: 
• Loop through each variant and download all associated images. 
• Save the images in the uniquely generated folder. 
5. Detect Duplicate Images: 
• Use the difPy library to detect duplicate images in the folder. 
• Identify and list lower-quality duplicates for removal or analysis. 
6. Store Duplicate Information: 
• Save the list of duplicates along with their corresponding product URLs to a CSV file. 
• Organize the CSV file by category for easy reference. 
7. Move Images to Final Directory: 
• Transfer all downloaded images, including detected duplicates, to a category-specific folder for 
long-term storage. 
This approach ensures that the process is automated, systematic, and organized, allowing for efficient 
management of large datasets involving product images. 
Business Value:  
1. Improved Marketplace Quality: 
By ensuring that all product images are distinct and accurately represent the product, GeM can 
maintain a high-quality marketplace, which is essential for buyer trust and satisfaction. 
2. Enhanced Seller Accountability: 
Sellers will be encouraged to adhere to platform policies, knowing that the system will flag any 
attempt to circumvent the rules. 

![Unstructured data analysis - Image duplication](https://github.com/user-attachments/assets/c4704a7f-5b3c-439c-ad0b-1e66644bf701)






