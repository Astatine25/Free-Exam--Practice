This README provides a comprehensive guide for using your Python-based scraping tool to extract exam preparation data.

A two-stage Python tool designed to automate the collection of exam questions, options, and community-voted answers. This is specifically optimized for AWS certifications like the **AIF-C01 (AWS Certified AI Practitioner)**.

## 📋 Features

* **Multi-threaded Scanning:** Rapidly searches through hundreds of discussion pages to find specific exam codes.
* **Intelligent Extraction:** Captures question text, multiple-choice options, and the "Most Voted" community answer.
* 
**Topic Grouping:** Automatically organizes links by Topic and Question number for structured studying.


* **Anti-Bot Headers:** Uses custom User-Agents and request delays to reduce the risk of IP blocking.

---

## 🛠️ Setup & Usage

### 1. Prerequisites

You will need a Python environment (Google Colab is recommended). Install the required libraries:

```bash
pip install requests beautifulsoup4 tqdm

```

### 2. Phase 1: Link Collection

Run the **Scraper Script**. This will crawl the provider's discussion board (e.g., Amazon) and identify all links related to your exam code.

* **Inputs:** `provider` (e.g., amazon), `exam code` (e.g., AIF-C01).
* 
**Output:** Generates a file named `AIF-C01_links.txt` containing all discovered discussion URLs.



### 3. Phase 2: Content Extraction

Run the **Stage 2 Scraper**. This script reads `AIF-C01_links.txt`, visits each URL, and pulls the actual question data.

* **Input:** The `.txt` file generated in Phase 1.
* **Output:** Generates `AIF-C01_Questions_Answers.txt` with formatted questions, options, and answers.

---

## 🧩 Code Architecture

The scraping process follows a structured data pipeline to move from a website URL to a local study guide:

### Key Components:

* **`Scraper` Class:** Manages the session and handles pagination logic to find the total number of discussion pages.
* 
**`extract_topic_question`:** Uses regular expressions to parse "Topic X Question Y" from URLs to ensure the output is sorted correctly.


* **`scrape_question_details`:** Targets specific HTML classes like `card-text` (questions) and `multi-choice-item` (options).

---

## ⚠️ Important Considerations

* **Rate Limiting:** ExamTopics employs aggressive anti-scraping measures. The scripts include `time.sleep()` intervals. Increasing the speed (more threads or less sleep) may result in a temporary IP ban.
* **"Most Voted" vs. Official:** This tool prioritizes the **Community Answer**. In many AWS exams, the community-voted answer is widely considered more accurate than the "official" one provided on the site.
* **Data Integrity:** If the script returns "None" or "Answer not found," you may have encountered a Cloudflare CAPTCHA. Open the site in your browser to clear the check.

---

## 📂 Output Format Example

The final output is structured for easy reading and importing into flashcard apps:

> **URL:** [https://www.examtopics.com/discussions/amazon/view/](https://www.google.com/search?q=https://www.examtopics.com/discussions/amazon/view/)...
> **QUESTION:** A company wants to use machine learning to predict...
> **OPTIONS:**
> * A. Amazon SageMaker
> * B. AWS Lambda
> 
> 
> **COMMUNITY ANSWER:** Most Voted: A

Would you like me to show you how to format this output into a **CSV file** so you can import it directly into **Anki** or **Quizlet**?
