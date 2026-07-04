# 🎬 Automated AI Viral Video Production & Cross-Platform Distribution Pipeline

An advanced, enterprise-grade **n8n automation workflow** that turns simple raw ideas into highly optimized, platform-specific short-form video ads. 

The pipeline ingests media via a **Telegram Bot**, orchestrates multimodal AI models (**OpenAI GPT-4o, Fal.ai NanoBanana, and Kie.ai VEO3**) to generate cinematic structures and high-fidelity video variations, and utilizes **Blotato** to instantly distribute the finalized assets simultaneously across 9 distinct social media platforms.

---

## 🛠️ System Architecture & Phase Logic

<img width="1144" height="688" alt="WhatsApp Image 2026-07-04 at 5 36 44 PM" src="https://github.com/user-attachments/assets/0ef7763c-8072-402d-8cf6-b4ff56565c2c" />


The pipeline operates deterministically through 5 distinct sticky-note bounded phases to ensure strict data validation, proper asset generation, and error-free publication:

[ Telegram Ingest ] ➡️ [ Phase 1: Storage & Log ] ➡️ [ Phase 2: NanoBanana Image Gen ]
⬇️
[ Platform Publish ] ⬅️ [ Phase 5: Blotato Blast ] ⬅️ [ Phase 4: VEO3 Video Render ] ⬅️ [ Phase 3: Scripting ]


### 📑 STEP 1 — Collect Idea & Image (Ingestion & Logging)
* **Trigger:** Instantly catches incoming message payloads, captions, and file arrays via a unified `Telegram Trigger`.
* **Asset Storage:** Raw binaries are transferred straight to **Google Drive** for secure cloud archival.
* **Database Ledger:** Logs unique image IDs, temporary tracking flags (`STATUS: EN COURS`), and raw textual contexts inside a master tracking spreadsheet via **Google Sheets**.

### 📑 STEP 2 — Create Image with NanoBanana (Computer Vision & Image Manipulation)
* **Visual Understanding:** Downloads the raw Telegram asset and parses it using `OpenAI Vision (ChatGPT-4o-Latest)` to extract exact styling markers, palettes, font structures, and brand attributes into structured **YAML**.
* **UGC Structuring:** An LLM-driven structured parser designs an incredibly realistic, unpolished User-Generated Content (UGC) photo prompt mimicking phone snapshots.
* **Generative Manipulation:** Dispatches asynchronous REST requests over to the `Fal.ai NanoBanana Edit` engine (`/fal-ai/nano-banana/edit`), holds via a 20-second wait hook, and pulls down the newly contextualized brand image asset.

### 📑 STEP 3 — Generate Video Ad Script (Structured Content Engineering)
* **Config Syncing:** Fetches global production properties (like core rendering model types) straight from the centralized spreadsheet configurations.
* **Master Schema Execution:** An advanced `LangChain AI Agent` consumes a rigid, multi-layered visual schema JSON mapping camera angles, lighting dynamics, particle effects, sound design, and explicit product transition cues.
* **Deterministic Parsing:** Employs a strict `Structured Output Parser` to isolate a stringified, perfectly escaped JSON contract featuring two exact parameters: `title` and `final_prompt`.

### 📑 STEP 4 — Generate Video with VEO3 (Video Rendering & Copywriting)
* **Temporal Generation:** Feeds the dynamic script parameters and the enhanced NanoBanana source image directly to the `Kie.ai VEO3 API` (`/api/v1/veo/generate`).
* **Rendering Poller:** Pauses execution state dynamically to accommodate cloud-side video synthesis, subsequently polling the record endpoint using the unique `taskId`.
* **Platform Constraints Optimization:** Passes the output text into `GPT-4o` to rewrite a highly captivating social media caption explicitly bound to an absolute hard limit of **under 200 characters**.

### 📑 STEP 5 — Auto-Post to All Platforms (Blotato Omnichannel Syndication)
* **Media Upload:** Streams the verified high-fidelity video asset straight into **Blotato's** storage infrastructure.
* **Parallel Publication Blast:** Fan-out architecture concurrently publishes the asset, dynamic caption, and platform privacy tokens to 9 separate targets:
  * 📱 **TikTok** & **Instagram Reels**
  * 🎥 **YouTube Shorts** (forced to `private` mode for administrative review)
  * 💼 **LinkedIn** & 👥 **Facebook Pages**
  * 🐦 **Twitter (X)**, 🧵 **Threads**, 🦋 **Bluesky**, & 📌 **Pinterest**
* **State Finalization:** Synchronizes execution results back through a 9-way `Merge Node`, updates the tracking spreadsheet status to `Published`, and drops a Telegram confirmation alert back to the original operator chat.

---

## ⚙️ Setup & Credentials Mapping

To activate this automation framework in your local n8n instance, ensure the following placeholders inside the workspace variables are updated:

### 🔑 Critical Placeholders to Update
1. **`Set: Bot Token (Placeholder)` Node:** Paste your live Telegram Bot API key inside the value field to avoid file retrieval path errors.
2. **Google Sheets Nodes:** 
   * Connect your Google Service Account or OAuth credentials.
   * Map your exact Spreadsheet File IDs and Sheet Name references across all logging, updating, and configuration reading blocks.
3. **Blotato Platform Nodes:** Verify your `accountId` and profile mapping references match your team's respective social account registrations on the Blotato dashboard backend.
4. **HTTP Request Nodes (Fal.ai & Kie.ai):** Ensure your custom `httpHeaderAuth` configurations contain valid Bearer or Authorization API tokens for `Fal.ai` and `Kie.ai` platforms.

---

## 🚀 Deployment Instructions

1. **Import Blueprint:** Copy the entire JSON array, open an empty n8n canvas layout, and press `Ctrl+V` (or choose **Import from File**) to paste the workflow structure.
2. **Resolve Dependencies:** Authorize and link your app credential managers (OpenAI, Google Workspace, Telegram Bot, Blotato, and raw HTTP header credentials).
3. **Test Ingestion:** Toggle the active switches, drop an image containing a product or scene along with a descriptive text string inside your Telegram Bot, and track live executions via the execution logs
