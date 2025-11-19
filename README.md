# NHS Number Validation – Power Apps Model-Driven App JavaScript Sample

This repository contains a JavaScript sample that validates **NHS numbers** on a  
Power Apps model-driven app form.

It not only checks that the NHS number is correctly formatted as `XXX-XXX-XXXX`,  
but also validates that the number itself is **mathematically valid** using the  
Modulus 11 checksum rules for NHS numbers.

This sample is part of the **Solution Sunday** series by **Howdang Rashid (Powercademy)**.

---

## 🎯 Scenario

In many healthcare solutions built on Power Platform, users must capture NHS numbers.  
If these numbers are entered incorrectly, it can cause:

- Data-quality issues  
- Matching/linking problems across systems  
- Compliance concerns  
- Incorrect patient records  

This sample enforces both **format** and **checksum** validation to ensure the NHS number  
is valid before the form is saved.

---

## 🧠 How the Code Works

The main entry point is the `validateNHSNumber(executionContext)` function.

Here’s what it does:

1. Retrieves the NHS number field using its **logical name**  
   (default in this sample: `ttd_nhsnumber` — you'll change this to match your own column).

2. Handles basic conditions:
   - Field missing → logs an error  
   - Field empty → clears notifications and exits  

3. Validates the **format**, ensuring it matches `XXX-XXX-XXXX`.

4. Removes dashes and confirms the underlying number:
   - Is 10 characters  
   - Contains only digits  

5. Computes the **checksum** via `isValidChecksum(nhsNumber)`:
   - Uses Modulus 11  
   - Validates the last digit matches the calculated check digit  
   - Rejects checksums of 10 (not valid in the NHS spec)

6. Uses `showErrorMessage` to surface errors on the form using setNotification.

If all validation passes, any existing notifications are cleared.

> 🔎 **Note:** This sample currently supports *string columns only*.

---

## 📁 Files in This Repository

- `nhs-number-validation.js`  
  Contains:
  - `validateNHSNumber(executionContext)`
  - `isValidChecksum(nhsNumber)`
  - `showErrorMessage(formContext, message)`

- `Screenshots/` *(optional)*  
  Screenshots showing form setup and validation behaviour.

---

## 🚀 How to Use This Sample

### 1️⃣ Adjust the Code for Your Column

Before uploading, open the JS file and replace: ""ttd_nhsnumber"

With the logical name of your NHS number column, e.g.: "new_nhsnumber"

If you don't update this, the script will try to validate the wrong field
(unless your column actually is ttd_nhsnumber).

### 2️⃣ Add the Script as a Web Resource

1. Go to **Power Apps Maker Portal** → **Solutions**  
2. Open or create a solution  
3. Select **+ New** → **More** → **Web resource**  
4. Upload **nhs-number-validation.js**  
5. Give it a meaningful name, e.g.  
   **NHS Number Validation Script**  
6. Set **Type:** JavaScript (JS)  
7. Save and publish the web resource  

---

### 3️⃣ Add the Library to Your Form

1. Open the form that contains your NHS number field  
2. Go to **Form libraries**  
3. Select **+ Add library**  
4. Add your uploaded **NHS Number Validation** script  
5. Save the form  

---

### 4️⃣ Register the Event Handler

1. Select the **NHS number field** on the form  
2. Go to the **Events** tab  
3. Click **+ Event handler**  
4. In the popup:  
   - Pick your **NHS Number Validation** library  
   - Set the **Function name** to:  

     ```text
     validateNHSNumber
     ```  

   - Ensure **Pass execution context** is checked  
5. Save and publish the form  

---

### 5️⃣ Test the Behaviour

Try entering different values:  

- ❌ **Wrong format** → should show a format error  
- ❌ **10 digits but bad checksum** → should show invalid NHS number  
- ✔ **Correct format + correct checksum** → form should save successfully  

This ensures your data remains clean and compliant.

---

### ⭐ Best Practices

- Always store NHS numbers as **strings**, not numeric values  
- Use a **namespace** if combining multiple scripts in one form  
- Keep **error messages** in one place for localisation  
- Add **comments** for maintainability  
- Test in a **sandbox environment** before production  

---

### 👤 About the Author

Created by **Howdang Rashid**,  
Power Platform Architect and founder of **Powercademy**.  

Part of the **Solution Sunday** series – weekly technical samples, patterns,  
and practical solutions for Power Apps professionals.  

Connect with me on LinkedIn:  
[https://www.linkedin.com/in/howdangrashid](https://www.linkedin.com/in/howdangrashid)
