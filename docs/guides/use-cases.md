# Use cases


# [`/nbstat`](../api-reference/endpoints/nbstat.md) 

### 🛠️ Filling the Gap between Macro and Micro Data
The [`/nbstat`](../api-reference/endpoints/nbstat.md) endpoint bridges a gap between:


- 🌍 **Macro-level data**, such as **News Inflationary Pressures Indices (NIPI)**: Measures inflation trends across major aggregates (e.g., Headline, Core, Food, Energy).

 
- 🧩 **Micro-level data**, such as detailed item-focused inflation news from the AMS Inflation NewsBot.


### Examples

#### Egg prices news in the US


```python
params = { 'location': 'US', 
           'txt': 'egg' } 
```

Returns, with 7-days and 30-days smoothing windows:


![Egg price News Sign](https://www.alternativemacrosignals.com/assets/img/github/us-egg-sign.png)

![Egg price News Volume](https://www.alternativemacrosignals.com/assets/img/github/us-egg-vol.png)

-----------


#### Rice price news in Japan
```python
params = { 'location': 'Japan', 
           'txt': 'rice' } 
```

![Rice price News Sign](https://www.alternativemacrosignals.com/assets/img/github/jp-rice-sign.png)

![Rice price News Volume](https://www.alternativemacrosignals.com/assets/img/github/jp-rice-vol.png)


#### Supply chain issues  

```python
params = { 'location': 'US', 
           'txt': 'supply chain' } 
```

![Supply chain News Sign](https://www.alternativemacrosignals.com/assets/img/github/us-suppl-sign.png)

![Supply chain News Volume](https://www.alternativemacrosignals.com/assets/img/github/us-suppl-vol.png)








### More Resources
🔗 Read our [blog](https://alt.ms/blog) for historical illustrations and extended case studies.

