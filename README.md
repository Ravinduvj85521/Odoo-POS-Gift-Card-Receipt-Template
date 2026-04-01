# Odoo 19 POS Thermal Receipt Gift Card Template

By default, Odoo generates Gift Cards as A4-sized PDF documents. If you are running a retail store and want to print gift cards directly from your 80mm POS thermal receipt printer, the default QWeb template will look tiny and unreadable.

This repository provides a custom QWeb XML template that forces the Odoo gift card into a narrow, continuous format optimized for 80mm thermal paper. 

## Features
* **80mm Optimized:** Uses inline CSS to constrain the width to a thermal-friendly 260px.
* **QR Code Integration:** Replaces the standard Code128 barcode (which often breaks or overlaps on long 14-character gift card codes) with a perfectly scaling, highly scannable QR Code.
* **Dynamic Logo:** Automatically pulls your company's logo from Odoo's General Settings.
* **Clean Typography:** Uses standard monospace fonts for a classic retail receipt look.

## Installation Instructions (UI Method)

You do not need to create a custom Python module to use this. You can apply it directly via the Odoo UI.

### Step 1: Create a Thermal Paper Format
To prevent Odoo from printing an A4 page with massive white margins, you must define a custom paper format.
1. Activate **Developer Mode** in Odoo.
2. Navigate to **Settings** > **Technical** > **Reporting** > **Paper Formats**.
3. Create a **New** format with the following settings:
   - **Name:** POS Receipt 80mm
   - **Format:** Custom
   - **Page Width:** 80.00
   - **Page Height:** 200.00 (or longer depending on preference)
   - **Orientation:** Portrait
   - **Margin Top / Bottom / Left / Right:** Set all to `1.00.`
   - **Header Spacing:** `0`
4. Go to **Settings** > **Technical** > **Reporting** > **Reports**, search for the `Gift Card` report, and assign this new Paper Format to it via the Advanced tab.

### Step 2: Apply the Custom QWeb Template
1. Navigate to **Settings** > **Technical** > **User Interface** > **Views**.
2. Search for the view named `loyalty.report_gift_card` (or `loyalty.gift_card_report` depending on your specific localization/version).
3. Open the record and click on the **Architecture** tab.
4. Delete the existing code and paste the XML code found in `gift_card_template.xml` from this repository.
5. *(Optional)* Update the physical address in the `<p>` tags to match your store's location.
6. **Save**.

## Troubleshooting
If your QR code prints as a blank box or broken image text, ensure your Odoo server is properly routing PDF image requests locally. You may need to check your `web.base.url` or `report.url` system parameters.
