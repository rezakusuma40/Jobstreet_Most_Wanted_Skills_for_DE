In this personal project, I scraped data engineer job vacancies from jobstreet to make a wordcloud visualization of the most wanted skills for data engineering.

I used BeautifulSoup on Jupyter Notebook, here is the link I scraped (it doesn't seems to change in the future):
https://www.jobstreet.co.id/id/data-engineer-jobs?sort=createdAt

As you can see, that is the jobstreet website for Indonesian job, it's already searching for data engineering job using "data engineer" keyword sorted by time posted.

There were many challenges in this project, the first was how to scrape all pages, I needed to create an iterating code that open and scrape all pages. Not only that, some data can only be scraped by opening the job vacancy's web page. while each page have 30 job vacancies.

The next problem was even more challenging, that was determining which job are true data engineering job to scrape. The result of "data engineer" keyword wasn't very accurate. Usually, we get about 1000 jobs when we search "data engineer" on jobstreet.co.id however many of them are actually other jobs such as data scientist, data analyst, software engineer, devops engineer, etc.. they also have varying titles so I had to manually create a list of possible data engineer job titles. Sadly, among those 1000 jobs, usually there are only 70-100 actual data engineering jobs.

The third challenge which was the biggest and most exciting for me (but also boring) was to get the skills necessary for data engineering. There were no tags specified for skills to scrape, all skills must be extracted from job description (it's a very long unstructured text). Python (or any other language I guess) doesn't have any built-in module to recognize data engineering skills like sql, python, etc. (understandable). So I had to manually create a dictionary of data engineering skills to search from the job description, which was way much longer than the previous title list.

Next is the data cleansing step. the result was 5 clean pandas dataframe. I then store them to PostgreSQL database, create data model and create report using Power BI.

Unfortunately, Not everything can be done by coding. there are some limitation of this project:

1. Each job vacancy had no distinct id to differentiate from each other, the most unique attribute was job vacancy's web page URL. that means if a job vacancy was posted more than once the code won't know it. Combining title and company name is also not unique enough.
2. Some job has title that looks as if it's data engineering job although it isn't, while some data engineering job isn't scraped because it use unrecognizable title. leading to errors in dataset.
3. It can't distinguish fraudulent job vacancy.
