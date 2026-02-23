# 🚀 Smart RSS-to-Notion Monitor

A production-ready automation workflow built with **n8n** that monitors RSS feeds (e.g., TechCrunch), filters for real-time updates, and synchronizes new articles into a **Notion** database with intelligent automated categorization.

---

## 📋 Features

* **Automated Polling**: Checks RSS feeds every 30 minutes using the `Schedule Trigger`.
* **Duplicate Prevention**: Advanced filtering logic ensures only articles published within the last 30 minutes are processed, preventing database clutter.
* **Smart Categorization**: Automatically tags articles based on keywords (e.g., distinguishing "Apple/Tech" from general news).
* **Data Normalization**: Cleans and formats raw RSS XML data into structured Notion properties (Title, URL, Date, Category).
* **Scalable Architecture**: Easily extendable to monitor multiple RSS sources simultaneously.

## 🛠 Tech Stack

* **n8n**: Workflow automation and orchestration.
* **Notion API**: Cloud-based database management.
* **RSS/XML**: Real-time data source.

## 🏗 Workflow Logic

The system follows a 5-step engineering pipeline:
1.  **Schedule**: Triggers the workflow at a fixed interval.
2.  **RSS Read**: Fetches the latest feed items from the source URL.
3.  **Filter**: A logic gate that only allows items where `pubDate` is greater than `now - 30 minutes`.
4.  **Edit Fields (Set)**: Maps RSS data to custom variables and applies conditional logic for tagging.
5.  **Notion**: Executes the `Create Database Page` operation to store the final result.

## 🚀 Getting Started

### 1. Prerequisites
* A running instance of **n8n** (Desktop, Cloud, or Docker).
* A **Notion** account with a database prepared (ensure you have columns for "Title", "URL", and "Tags").
* A Notion **Internal Integration Token** (Create one at [notion.so/my-integrations](https://www.notion.com/my-integrations)).

### 2. Installation
1.  Download the `workflow.json` file from this repository.
2.  In your n8n dashboard, create a new workflow.
3.  **Import** the JSON file or simply `Ctrl+V` the code into the editor.

### 3. Configuration
1.  Open the **Notion Node** and create a new credential using your Secret Token.
2.  **Share** your Notion database with the integration you created (Top right: Share -> Add Integration).
3.  Select your Database ID from the dropdown menu in n8n.
4.  Switch the toggle to **Active** to start the automation.

## 📝 Customization

You can modify the auto-tagging logic in the `Edit Fields` node using the following expression:

```javascript
{{ $json.title.toLowerCase().includes('apple') ? '🍎 Apple News' : '💻 General Tech' }}