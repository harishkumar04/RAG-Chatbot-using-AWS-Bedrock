# 🧩 Building My RAG Chatbot with Amazon Bedrock

This repository documents how I built a **Retrieval-Augmented Generation (RAG)** project using **Amazon Bedrock**.  
The goal: create a chatbot that can use my own documents stored in **Amazon S3**, retrieve them intelligently with a **vector store**, and then generate natural, context-aware responses using AI models.  

<img width="720" height="395" alt="Screenshot 2025-09-01 at 5 50 42 PM" src="https://github.com/user-attachments/assets/b2912705-a48c-452d-a1dc-bd1f3cca25a5" />

---

## 🌍 Step 1: Setting the Region
I started by switching my AWS region to **Ohio (`us-east-2`)**.  
Not every region supports Bedrock models, so this ensures I get the right hardware and AI access.

---

## 📚 Step 2: Creating the Knowledge Base
Inside **Amazon Bedrock**, I went to:
**Bedrock → Builder → Knowledge Base**

<img width="601" height="333" alt="Screenshot 2025-10-01 at 10 56 37 PM" src="https://github.com/user-attachments/assets/90a7c967-fdcc-496b-ad82-c05b294b1bda" />

Here’s why I went with a **vector store** instead of traditional keyword search:

- A keyword search is like asking a librarian for a book by exact title.  
- A vector store is like asking a librarian who also *understands context* and brings you related material.  

For example:  
If I search **“cat food”**, a keyword search only returns items labeled *cat food*.  
A vector store search knows it’s related to *pets* and might also suggest *toys, litter, or grooming products*.  

That’s why vector search is so powerful for RAG — it captures intent, not just words.

**Give the knowledge base a name and then a Service role**

<img width="592" height="341" alt="Screenshot 2025-10-01 at 10 57 47 PM" src="https://github.com/user-attachments/assets/08b9c0a7-52ef-42b9-a9ad-c1cadf3c5da1" />

---
## 🪣 Step 3: Setting Up the Data Source

### 3.1 Creating an S3 Bucket
I created a new bucket and named it:

```text
s3-research-2
```
<img width="600" height="178" alt="Screenshot 2025-10-01 at 10 58 30 PM" src="https://github.com/user-attachments/assets/cc68f890-3456-4e46-9f9e-3b15e4c05c17" />

I kept the encryption and key settings as the defaults.

### 3.2 Uploading Documents

Next, I uploaded my files into the bucket:
**S3 → Open bucket → Upload → Add files**

<img width="839" height="509" alt="Screenshot 2025-09-01 at 3 47 51 PM" src="https://github.com/user-attachments/assets/8d1a7bd5-e14e-4266-b957-51a1d936318f" />

<img width="1247" height="641" alt="Screenshot 2025-09-01 at 4 37 35 PM" src="https://github.com/user-attachments/assets/ecb7f96d-18d6-487b-a55d-1b6c9b628c69" />

This is the raw data my chatbot will eventually pull answers from.

<img width="1186" height="472" alt="Screenshot 2025-09-01 at 5 24 47 PM" src="https://github.com/user-attachments/assets/c8749d81-0d64-45ed-b90d-4f91b3e22b4a" />
---

## 🤖 Step 4: Connecting to AI Models

A knowledge base alone just returns snippets of text.
The **AI model** makes it conversational — it understands questions and generates natural answers instead of dumping raw text.

If I ever want *only* raw snippets, I can just **turn off "Generate Responses"** in the Bedrock chatbot interface.

### 4.1 Enabling Model Access

I went to **Bedrock → Model access → Enable Specific Model** and selected the models I wanted to use.
That gave my chatbot the brainpower to interpret and respond to queries.

---

## 🔄 Step 5: Syncing Data

At this point, my knowledge base existed but was empty.
To load my S3 data into **OpenSearch Serverless (vector store)**, I synced the data:

* **Bedrock → Data Source → Sync**

Once synced, I tested the knowledge base by selecting a model and asking it questions.

---

## 💬 Step 6: Testing the Chatbot

I tried different types of questions:

* Relevant ones → It pulled answers directly from my documents.
<img width="1167" height="530" alt="Screenshot 2025-09-01 at 5 31 54 PM" src="https://github.com/user-attachments/assets/6b519582-643c-475b-9c6d-2509e63378c7" />

* Irrelevant ones → It politely said the knowledge base had nothing to offer.

<img width="584" height="384" alt="Screenshot 2025-09-01 at 5 29 51 PM" src="https://github.com/user-attachments/assets/2063884d-e25a-4f7c-bc59-1d0e3c59abcc" />

This gave me confidence that the system was both accurate and safe.

---

## 🎯 Step 7: Improving the Responses

I didn’t stop there. To make the chatbot even better, I explored:

* **Custom prompts** → Tailoring the style of responses.
<img width="555" height="217" alt="Screenshot 2025-09-01 at 5 37 03 PM" src="https://github.com/user-attachments/assets/2809f787-195a-40cb-9566-a2ce69fac179" />

<img width="575" height="657" alt="Screenshot 2025-09-01 at 5 37 09 PM " src="https://github.com/user-attachments/assets/4ceff91d-a58c-4a3d-8398-84eefb24ff25" />

* **Chunk sizes** → Adjusting how the documents are split before embedding.

  <img width="583" height="538" alt="Screenshot 2025-09-01 at 5 36 54 PM" src="https://github.com/user-attachments/assets/0af0ccdf-19b2-41b7-87fa-7deab3d530d7" />

* **Source weights** → Controlling which data sources are prioritized.

These tweaks help generate more precise, human-like answers.

---

## ✅ Final Thoughts

This project showed me how simple it can be to combine:

* **Amazon S3** for storing my data
* **Vector stores** for smart retrieval
* **Amazon Bedrock models** for generating conversational answers

The result: a working **RAG chatbot** that feels intelligent and context-aware.
