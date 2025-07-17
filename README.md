# 📄 Resume Parser + Dashboard (AWS Powered)

A fully serverless application that allows users to **upload resumes** (PDF), **extract key information** like name, email, and skills using **AWS Textract**, and store it in **DynamoDB** — all visualized on a **dashboard webpage**. Built with **S3 + Lambda + API Gateway + DynamoDB**.

---
### Note - I have deleted all the functions and services to avoid any cost from AWS. But i have documented all the steps and procedure to re-create this webapp again easily. Just go throught the steps carefully and enjoy your resume parser.

## What is a Resume Parser??

A resume parser is a software tool or script that automatically extracts structured information from a resume (CV), which is typically in PDF, DOCX, or plain text format.

##🧠 What It Does

Instead of a human manually reading resumes to find:

👤 Name
📧 Email
📞 Phone Number
💼 Work Experience
🎓 Education
💡 Skills

…a resume parser reads the document and converts that unstructured content into structured data — usually in JSON or key-value form.

##📦 Why It's Useful

✅ Saves time – No manual copy-pasting from PDF to form.
✅ HR automation – Auto-screen candidates based on skills.
✅ ATS (Applicant Tracking System) – Integrates with HR systems.
✅ Searchable – Makes resume data filterable and sortable.
✅ Data Insights – Enables analytics like common skills, experience range, etc.

## 🚀 Features

- Upload resumes (PDF) securely via pre-signed URL.
- Extract name, email, and skills using AWS Textract.
- Store parsed data in DynamoDB.
- Live Dashboard: View parsed resume details.
- 100% Serverless – Scalable & Cost-efficient.

---

## 🧠 What This Project Actually Does

✅ When a PDF resume is uploaded:
1. It goes to a secure S3 bucket via a **pre-signed URL**.
2. A Lambda function is triggered via **S3 event**.
3. Lambda uses **Amazon Textract** to extract text.
4. It parses for basic fields: `Name`, `Email`, `Skills`.
5. The data is saved to **DynamoDB**.
6. A dashboard frontend calls another Lambda (via API Gateway) to **read** all resumes and display in a table.

---

## 📂 Tech Stack

| Layer         | Service            |
|---------------|--------------------|
| Upload Logic  | S3 (with pre-signed URLs) |
| Compute       | AWS Lambda (3 functions) |
| API           | Amazon API Gateway (2 API) |
| OCR           | AWS Textract       |
| DB            | DynamoDB           |
| Frontend      | HTML + JS  |

---

## 🛠️ How to Set Up (Step-by-Step)

### 1️⃣ Create S3 Bucket
- Enable **static website hosting**.
- Make sure to allow `PUT` access via bucket policy for pre-signed uploads.
<img width="1897" height="925" alt="Screenshot 2025-07-15 235059" src="https://github.com/user-attachments/assets/66b76ccd-980f-4325-a3a9-b3ac485d3797" />
<img width="1919" height="977" alt="Screenshot 2025-07-15 235034" src="https://github.com/user-attachments/assets/1e6c92be-67a5-4d90-930c-413377cbde07" />
<img width="1915" height="976" alt="Screenshot 2025-07-16 001427" src="https://github.com/user-attachments/assets/9c45a76a-ebf2-4f57-abf6-762dc9c9401f" />
<img width="1919" height="983" alt="Screenshot 2025-07-16 001437" src="https://github.com/user-attachments/assets/c67dd431-3032-490a-bac2-abd4bdc2656e" />
<img width="1919" height="980" alt="Screenshot 2025-07-16 001444" src="https://github.com/user-attachments/assets/454d9983-717f-448b-9526-99850f7babaa" />
<img width="1919" height="982" alt="Screenshot 2025-07-16 001508" src="https://github.com/user-attachments/assets/99babe99-7e53-42d8-a7be-2ccca27bb7a5" />
<img width="1919" height="977" alt="Screenshot 2025-07-16 003817" src="https://github.com/user-attachments/assets/1cd54a0f-7881-446f-8a52-a0363d7b0ac2" />
<img width="1919" height="977" alt="Screenshot 2025-07-16 003903" src="https://github.com/user-attachments/assets/ec250a43-a32b-4300-9ba9-d02ed0e9b5fe" />

---

### 2️⃣ Create Lambda functions. 
1. Resume-upload-url function -
   
   <img width="1919" height="978" alt="Screenshot 2025-07-15 235529" src="https://github.com/user-attachments/assets/6b472f36-d307-4635-89b5-02a1a7f0d6c6" />
   <img width="1919" height="983" alt="Screenshot 2025-07-15 235619" src="https://github.com/user-attachments/assets/38089b87-8045-4a62-8f39-92a670dc633c" />
   <img width="1919" height="979" alt="Screenshot 2025-07-15 235637" src="https://github.com/user-attachments/assets/7480d718-d683-4e41-aa5b-89a0e3ea96e6" />
   <img width="1917" height="980" alt="Screenshot 2025-07-15 235709" src="https://github.com/user-attachments/assets/d334d957-d359-40a5-b4c7-c08d3b65616a" />
   <img width="1919" height="978" alt="Screenshot 2025-07-15 235736" src="https://github.com/user-attachments/assets/f78edf4c-07d8-4e73-a003-af865ebaa732" />
   <img width="1919" height="977" alt="Screenshot 2025-07-15 235753" src="https://github.com/user-attachments/assets/e07c3055-9085-4617-bb5a-150ae5642a8a" />
   <img width="1919" height="979" alt="Screenshot 2025-07-16 001124" src="https://github.com/user-attachments/assets/73b07a14-d2da-46f2-8f57-ed213a8ca71f" />

lambda code- 

  <img width="739" height="950" alt="image" src="https://github.com/user-attachments/assets/400a2fe3-62ac-4113-b624-955c1dc15605" />
  <img width="719" height="268" alt="image" src="https://github.com/user-attachments/assets/15b93307-b2ba-4310-a58b-a5d739df37eb" />

3. Uploaded-resume function -
   
   <img width="1919" height="979" alt="Screenshot 2025-07-16 001927" src="https://github.com/user-attachments/assets/513a3116-f0ef-4b58-b3cc-0032445d910e" />
   <img width="1919" height="978" alt="Screenshot 2025-07-16 010213" src="https://github.com/user-attachments/assets/392ed57c-c864-4514-9973-dfa1e5c10b96" />
   <img width="1919" height="978" alt="Screenshot 2025-07-16 001958" src="https://github.com/user-attachments/assets/4187bf00-27d4-4826-8460-8f8f237c13ee" />
   <img width="1919" height="978" alt="Screenshot 2025-07-16 002105" src="https://github.com/user-attachments/assets/83463a4b-a751-41ea-9fb1-3f4380bfcf55" />
   <img width="1919" height="980" alt="Screenshot 2025-07-16 002226" src="https://github.com/user-attachments/assets/7518df12-9361-4676-a6c1-0d922ddb0e67" />
   <img width="1919" height="978" alt="Screenshot 2025-07-16 002240" src="https://github.com/user-attachments/assets/002b8f73-adc6-429a-9d42-aaa927e0cc73" />
   <img width="1919" height="977" alt="Screenshot 2025-07-16 003903" src="https://github.com/user-attachments/assets/a8d55026-b073-47a2-a23a-9afc99f3e017" />
   <img width="1916" height="983" alt="Screenshot 2025-07-16 002414" src="https://github.com/user-attachments/assets/1e7070e4-bbcd-4f87-bbc2-5f4740695c28" />
   <img width="1919" height="977" alt="Screenshot 2025-07-16 002620" src="https://github.com/user-attachments/assets/69b681dc-b75a-4083-aa0a-62f62ea44f21" />
   <img width="1919" height="973" alt="Screenshot 2025-07-16 002641" src="https://github.com/user-attachments/assets/80f79cbd-9c27-483a-8669-a563d118d3bd" />
   <img width="1919" height="985" alt="Screenshot 2025-07-16 004455" src="https://github.com/user-attachments/assets/67cf18bf-6e5a-406a-a2dc-e4129c21ad70" />
   <img width="1919" height="984" alt="Screenshot 2025-07-16 004519" src="https://github.com/user-attachments/assets/b2738de6-189f-4ac5-ab70-30518128a815" />            

lambda code - 

  <img width="1041" height="854" alt="image" src="https://github.com/user-attachments/assets/b0251bf8-dde6-4ccd-b5a3-d8dbe0d8285b" />
  <img width="1033" height="318" alt="image" src="https://github.com/user-attachments/assets/2f1bf399-3cc0-4b10-a168-f0f726eff2e1" />

4. Get-resume Function -

   <img width="1919" height="975" alt="Screenshot 2025-07-16 011826" src="https://github.com/user-attachments/assets/3b973654-7c1b-4bbf-90b8-73ac40e5b2ef" />
   <img width="1919" height="981" alt="Screenshot 2025-07-16 013151" src="https://github.com/user-attachments/assets/3c6cd816-e4bb-4b33-9072-49e8f0f033ae" />
   <img width="1919" height="979" alt="Screenshot 2025-07-16 012130" src="https://github.com/user-attachments/assets/209670e9-b212-4dab-85af-a268ed60a47d" />
   <img width="1919" height="988" alt="Screenshot 2025-07-16 012143" src="https://github.com/user-attachments/assets/0ae4cab5-0e30-46b1-ab0d-dc538324acac" />
   - Use `dynamodb.scan()` to get all resumes.
   <img width="1919" height="981" alt="Screenshot 2025-07-16 014405" src="https://github.com/user-attachments/assets/8d239b83-86e9-41bb-af6d-6e60e298b6e3" />

lambda code - 
<img width="936" height="788" alt="image" src="https://github.com/user-attachments/assets/45aa1ac2-4228-431f-8911-3129b544bccf" />

---

### 3️⃣ Set Up Dynamodb -
- Lambda uses `boto3.client("textract")` to extract text.
- Parse out name, email, and skills.
- Store the info in DynamoDB.

<img width="1919" height="980" alt="Screenshot 2025-07-16 001742" src="https://github.com/user-attachments/assets/c6ee4bf3-bc0e-47da-a248-26eb99ca0035" />
<img width="1919" height="981" alt="Screenshot 2025-07-16 001843" src="https://github.com/user-attachments/assets/6a0437c3-e960-4b7a-8953-a9495f89e1e1" />
<img width="1919" height="984" alt="Screenshot 2025-07-16 003231" src="https://github.com/user-attachments/assets/33dc0601-cf9c-44a2-ae8e-7fe783d323d7" />


✅ Make sure Lambda has these IAM permissions:
- `textract:DetectDocumentText`
- `dynamodb:PutItem`

---

### 4️⃣ Create a API's -

1. Upload-url-api -

   <img width="1919" height="978" alt="Screenshot 2025-07-16 000011" src="https://github.com/user-attachments/assets/2c12a92e-1d42-4b07-ba33-0f98cb3dd859" />
   <img width="1919" height="979" alt="Screenshot 2025-07-16 000045" src="https://github.com/user-attachments/assets/376618a2-8cbd-4672-be02-447fa9d928f3" />
   <img width="1919" height="968" alt="Screenshot 2025-07-16 000138" src="https://github.com/user-attachments/assets/45ece3af-31b9-4173-96f3-5d96c4c49595" />
   <img width="1919" height="977" alt="Screenshot 2025-07-16 000230" src="https://github.com/user-attachments/assets/5a924b17-7fd4-4c70-b267-f7daec0e687f" />
   <img width="1919" height="985" alt="Screenshot 2025-07-16 000319" src="https://github.com/user-attachments/assets/e5ded3c3-3494-46aa-b09a-1e86a18616d5" />
   <img width="1918" height="980" alt="Screenshot 2025-07-16 000218" src="https://github.com/user-attachments/assets/01431bfd-a83f-40be-863b-052588442d74" />
   <img width="1919" height="980" alt="Screenshot 2025-07-16 000331" src="https://github.com/user-attachments/assets/2e3f4c53-0e6b-401d-a1a3-0303d4e03486" />

2. Dashboard-api -

   <img width="1919" height="978" alt="Screenshot 2025-07-16 012220" src="https://github.com/user-attachments/assets/623e1a7b-a388-4f63-8f91-decdc74d18c2" />
   <img width="1919" height="982" alt="Screenshot 2025-07-16 012235" src="https://github.com/user-attachments/assets/4959894c-88e8-495a-98de-baad0838be51" />
   <img width="1919" height="983" alt="Screenshot 2025-07-16 012255" src="https://github.com/user-attachments/assets/67a777b1-80ec-422b-a72e-413e758e6aab" />
   <img width="1917" height="977" alt="Screenshot 2025-07-16 012333" src="https://github.com/user-attachments/assets/4713f193-64ff-4f7a-81e0-79a005694476" />


---

### 5️⃣ Frontend (HTML + JS)

<img width="1918" height="1029" alt="image" src="https://github.com/user-attachments/assets/0f8d018d-957b-4215-aed8-5f83cd16f89f" />


---

### 6️⃣ Fix CORS Error (Important)
If you see:
```
Access to fetch at... blocked by CORS policy
```
✅ Make sure **API Gateway** Lambda integrations return this:
```json
"Access-Control-Allow-Origin": "*"
```
✅ Also **enable CORS in Gateway settings** (GUI > CORS > Enable for All).
✅ And check if your S3 bucket has CORS policy updated if not go through step 1 carefully

### 7️⃣ And if you see Errors like unauthorized access to textract, dynamodb or S3 bucket access denied:
   
    ✅Then check if your lambda has an inline policy attack for textract , dynamodb and S3 if not then go through step 2 carefully.
---

## 💡 Unique Value / Resume-Worthy

This project demonstrates:
- 🔐 Secure upload using **pre-signed S3 URLs**
- 📄 OCR document parsing with **AWS Textract**
- 🧠 Serverless data pipeline using Lambda & API Gateway
- 📊 Dashboard with real-time updates
- 💼 Real-world workflow that scales – perfect for HR, ATS, job portals, etc.

---


## 🧠 Author  
Made by **Ujjwal Wadhai**
— Let’s connect on [LinkedIn](www.linkedin.com/in/ujjwal-wadhai)

