📌 QRPrompt – QR Codes with Restricted AI Prompts
🎯 Project Goal

QRPrompt is an open standard where a QR code on a product or object opens an AI app (e.g., ChatGPT, Grok) with a predefined system prompt.
The AI runs in “fact-only” mode – it uses only the JSON data provided by the manufacturer.
If the information is missing, the AI must refuse to answer.

✅ Benefits

No hallucinations

Fast access to reliable product data

Safer use for medicine, food, childcare

Interactive help instead of static manuals

🔗 QR Link Format

A single scan/click opens the QRPrompt handler, fetches the JSON data, and runs the AI in restricted mode (no internet browsing, no external knowledge beyond the provided file).


<pre><code>qrprompt://run?url=direct_link_to_JSON</code></pre>

<pre>qrprompt://run?url=https://raw.githubusercontent.com/qr-prompt/.github/e3521ee07e8594087a411b5943e22bbf5cc3f428/profile/qrprompt-json.json
</pre>

<ul>
  

<li> The app fetches the JSON from the given URL. </li>

<li> QR codes stay short and robust. </li>
<li>For additional obscurity, JSON file names can be encoded (for example using Base64 or hex).</li>

  
</ul>

<h2>Example JSON </h2>
<pre><code>{
  "version": "1.0",
  "command": "qrprompt",
  "meta": {
    "product_name": "Widget X"
  },
  "data": [
    { "mode": "url", "type": "json", "url": "https://example.com/product.json" },
    { "mode": "url", "type": "json", "url": "https://example.com/leaflet.json" },
    { "mode": "url", "type": "json", "url": "https://example.com/nutrition.json" }
  ],
  "policy": {
    "offline_only": true,
    "restrict_to_input": true,
    "disallow_external_knowledge": true
  },
  "prompt": {
    "system": "You are an assistant restricted to the provided JSON data. Do not browse the internet or use external knowledge. If data is missing, answer exactly: 'Not provided'. After loading the data, do not summarize or answer yet. Your first message must be exactly: \"Waiting for your questions about '{{product_name}}'?\". During the conversation, answer only from the input data."
  }
}
</code></pre>

<h2>Workflow</h2>
<p>
  <img src="./json-apka.png" alt="QRPrompt Workflow (JSON from URL + explicit policy)" width="600" />
</p>

<h2>Example Use Case — Food Products</h2>
<ul>
  <li>Context strictly limited to product JSON (ingredients, calories, allergens…)</li>
  <li>Typical questions: “How much protein per serving?”, “Does it contain gluten?”, “Is it vegan?”</li>
  <li>AI refuses when data is missing (“Not provided”).</li>
</ul>

<h2>Other Applications</h2>
<ul>
  <li><strong>Medicine</strong> — dosage, side effects, contraindications (with doctor referral)</li>
  <li><strong>Electronics/Appliances</strong> — manuals, error codes, accessories</li>
  <li><strong>Books</strong> — summaries, motifs, related authors</li>
  <li><strong>Travel</strong> — attractions, maps, local transport</li>
  <li><strong>Museums/Zoo</strong> — history, facts, education</li>
  <li><strong>Fashion</strong> — fabric composition, washing, styling</li>
  <li><strong>Furniture</strong> — assembly, cleaning, arrangements</li>
  <li><strong>Cosmetics</strong> — ingredients, allergy safety</li>
  <li><strong>Toys/Games</strong> — rules, variants, FAQ</li>
  <li><strong>Plants</strong> — watering, sunlight, diseases</li>
  <li><strong>Cars</strong> — dashboard lights, servicing, specs</li>
  <li><strong>Events</strong> — program, artists, venue maps</li>
  <li><strong>Finance/Contracts</strong> — policies, conditions, procedures</li>
</ul>

📱 Example QR Code (Prototype)

Below is a prototype QR code that demonstrates how QRPrompt could work today:

<p align="center"> <img src="./qr-code.png" alt="QRPrompt Example QR" width="300"/> </p>
Notes

The QR code is long because the current format directly encodes the entire system prompt and policy into the link.

This version is meant to showcase the concept — scanning the QR opens ChatGPT with strict rules (context = JSON file only, no internet, no hallucinations, no medical advice).

In the future, this can be simplified:

the QR would only contain a short qrprompt:// link,

the assistant would fetch the JSON + policy from the server,

keeping QR codes short, robust, and easier to generate.

⚠️ Important: This QR is for demonstration purposes only. It shows the potential of QRPrompt but is not yet optimized for production use.
⚠️ Limitation: This currently only works when the ChatGPT app (or web) supports direct links from OpenAI. Without this feature, the link will not be executed automatically.

<p align="center"> <img src="./test.jpg" alt="QRPrompt Example QR" width="300"/> </p>

<h2>Vision</h2>
<p>
  We believe AI interactions should be as easy as scanning a QR code—bringing
  safety, transparency, and interactivity to everyday products.
</p>

<hr/>

