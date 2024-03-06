```
banner
```
# Crawling Data 
### Web crawler 
- Use cases:
	- Monitoring Competitor Prices 
	- Monitoring the Product Catalogue 
	- Social media and news monitoring 
- Tools
	- Beautifulsoup 
	- Selenium 
- Projects
	- Choose a task 
	- Define: exp: sentiment analysis on social network's post
	1. Crawl data 
	2. Extract data (text, image) 
	3. Preprocessing 
	4. Annotate (2 annotators, small data)
		- Build annotation guideline 
		- Annotate 
		- Annotator agreement 
	5. Build model (use existing model)
	6. Train models, tune param
	7. Visualize results
	8. Build demo
	9. Presentation 
### Data Crawling System Architecture

### Common problem 
##### Data Extraction 
- Table in slide 
- Nên dùng XPath nhiều hơn vì truy vấn dữ liệu dễ hơn @_@ -> Học cách dùng XPath

##### Boilerplate removal 
- The task of seperating main text in a Web page from the remaining content 

##### Data Duplication 
- Non-structure data: Text/Image/Audio/Video 
- Structure data: Multiple fields 

<h5>Avoid getting blocked</h5>
- How do websites dectect and block: 
	1. Monitoring traffic
	2. Monitor users with high activity levels 
	3. Activities follow a pattern 
	4. Check your browser and PC
- How to avoid:
	1. Using proxy/rotating IP 
	2. Rotating User Agents 
	3. Using Headless Browsers 
	4. Do it slowly 