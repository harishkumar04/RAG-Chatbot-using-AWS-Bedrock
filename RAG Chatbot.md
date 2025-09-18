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

Here’s why I went with a **vector store** instead of traditional keyword search:

- A keyword search is like asking a librarian for a book by exact title.  
- A vector store is like asking a librarian who also *understands context* and brings you related material.  

For example:  
If I search **“cat food”**, a keyword search only returns items labeled *cat food*.  
A vector store search knows it’s related to *pets* and might also suggest *toys, litter, or grooming products*.  

That’s why vector search is so powerful for RAG — it captures intent, not just words.

---

## 🪣 Step 3: Setting Up the Data Source

### 3.1 Creating an S3 Bucket
I created a new bucket and named it:

```text
s3-research-2
```

I kept the encryption and key settings as the defaults.

### 3.2 Uploading Documents

Next, I uploaded my files into the bucket:
**S3 → Open bucket → Upload → Add files**

This is the raw data my chatbot will eventually pull answers from.

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
* Irrelevant ones → It politely said the knowledge base had nothing to offer.

This gave me confidence that the system was both accurate and safe.

---

## 🎯 Step 7: Improving the Responses

I didn’t stop there. To make the chatbot even better, I explored:

* **Custom prompts** → Tailoring the style of responses.
* **Chunk sizes** → Adjusting how the documents are split before embedding.
* **Source weights** → Controlling which data sources are prioritized.

These tweaks help generate more precise, human-like answers.

---

## ✅ Final Thoughts

This project showed me how simple it can be to combine:

* **Amazon S3** for storing my data
* **Vector stores** for smart retrieval
* **Amazon Bedrock models** for generating conversational answers

The result: a working **RAG chatbot** that feels intelligent and context-aware.
