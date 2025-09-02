# Use cases


# [`/nbstat`](../docs/api-reference/endpoints/nbstat) 

### 🛠️ Filling the Gap between Macro and Micro Data
The `/nbstat` endpoint bridges the gap between:


- 🌍 **Macro-level data**, such as **News Inflationary Pressures Indices (NIPI)**: Measures inflation trends across major aggregates (e.g., Headline, Core, Food, Energy).

 
- 🧩 **Micro-level data**, such as detailed item-focused inflation news from the AMS Inflation NewsBot.


---

### Practical Applications of `/nbstat`

#### ⚡ 1. Identify Specific Inflation Shocks
It's impossible to pre-build time series for every future shock (e.g., egg prices, home insurance, pandemics). However, by leveraging **AMS historical news archives and LLMs**, you can:
- Retrieve historical news mentioning a specific keyword (e.g., `"egg prices"`) and:
  - Analyze how "inflation signs" (positive/negative) for this query evolved over time  
  - Track how reporting volume changed across specific periods  
- Smooth historical data as needed: The endpoint provides **30-day and 7-day rolling averages** by default, but daily statistics are available for custom analysis.

---



#### 💡 2. Understand Inflation's Root Causes
Break down macro-level inflation aggregates (e.g., Energy Prices) to identify the driving components:
- Example: If energy prices are rising, analyze sector-specific contributors like **electricity costs**.

---

### Key Insight
Data accessed through `/nbstat`:
- Provides timely, granular insights into macro and micro trends.
- Supports custom queries tailored to specific industries, products, or phrases to reveal critical inflation signals.

---

### More Resources
🔗 Read our [blog](https://alt.ms/blog) for historical illustrations and extended case studies.

