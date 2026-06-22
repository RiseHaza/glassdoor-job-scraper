[Glassdoor Job Scraper](https://apify.com/newbs/Glassdoor-Job-Scraper?fpr=data)

## Others Job Scrapers ⚙️

[RemoteOk Premium Job Scraper](https://apify.com/newbs/RemoteOk-Premium-Job-Scraper).

[Craiglist Scraper Premium](https://apify.com/newbs/craiglist-scraper-premium).

[Indeed Job Scraper](https://apify.com/newbs/Indeed-Job-Scraper).

## Input

The actor takes in the following input:

- `jobTitle` (required) - The title of the job to search for.
- `location` (required) - The location where the job search will be performed.
- `numberOfPages` (required) - The number of job pages listings to scrape.
- `globalTimeoutSecs` (optional) - The maximum time the actor will run for. The default value is 300 seconds.

## Output

The actor outputs an array of objects, where each object represents a single job listing. The object includes the following details for each job listing:

- `jobTitle` - The title of the job listing.
- `companyName` - The name of the hiring company.
- `location` - The location of the job.
- `salary` - The salary information, if available.
- `jobDescription` - The description of the job listing.
- more below in the example output

## Usage

To use this actor, you can set up a task on Apify and configure the input parameters as desired. Once the task is started, the actor will scrape the specified number of job listings for the specified job title and location, and output the details in the format described above.

### Example Input

```
{
  "jobTitle": "Software Engineer",
  "location": "San Francisco",
  "numberOfPages": 1,
  "globalTimeoutSecs": 300
}
```

### Example Output

```
[
{
	"title": "DevOps Engineer",
	"url": "https://www.glassdoor.co.uk/job-listing/devops-engineer-adinmo-JV_KO0,15_KE16,22.htm?jl=1008933789604",
	"salary": "50000$ - 70000$ a year",
	"datePosted": "2023-10-18T00:00:00",
	"employmentType": "FULL_TIME",
	"validThrough": null,
	"employer": "AdInMo",
	"employerLogo": "https://media.glassdoor.com/sql/3615623/adinmo-squarelogo-1598033928727.png",
	"employerUrl": "https://www.glassdoor.com/Overview/Working-at-AdInMo-EI_IE3615623.11,17.htm",
	"location": null,
	"region": null,
	"country": "United Kingdom",
	"latitude": null,
	"longitude": null,
	"description": "This is a great time to join Team AdInMo to help us grow and scale our in-game advertising platform where you will be collaborating with our SDK, database and architecture teams to implement best practices, systems and tools in the DevOps toolchain.  You will have responsibility for the AdInMo infrastructure with the goal to deliver a robust and scalable solutions with a focus on reliability, resiliency, performance and security. You’ll be working with big data, ad tech and game developers in a rapidly scaling start-up environment.  Part-time/Full-time: UK or Remote (Europe)",
	"salaryCurrency": "GBP",
	"estimatedSalary": null,
	"baseSalary": null,
	"jobLocation": {
		"@type": "Place",
		"address": {
			"@type": "PostalAddress",
			"addressRegion": null,
			"addressCountry": {
				"@type": "Country",
				"name": "United Kingdom"
			}
		},
		"geo": {
			"@type": "GeoCoordinates",
			"latitude": 54,
			"longitude": -2
		}
	},
	"educationRequirements": {
		"@type": "EducationalOccupationalCredential",
		"credentialCategory": ""
	},
	"experienceRequirements": {
		"@type": "OccupationalExperienceRequirements",
		"monthsOfExperience": "",
		"description": "SDKs"
	},
	"experienceInPlaceOfEducation": null,
	"industry": "Media & Communication",
	"jobBenefits": null,
	"directApply": null,
	"employerDetail": {
		"id": 3615623,
		"industry": "Video Game Publishing",
		"industryId": 200083,
		"sector": "Media & Communication",
		"sectorId": 10016,
		"size": "1 to 50 Employees",
		"activeStatus": "INACTIVE",
		"location": "Remote",
		"locationId": 11048,
		"locationType": "S",
		"name": "AdInMo Ltd",
		"profileId": 1824280,
		"eepStatus": "Non-sponsored"
	}
}
]
```

## Disclaimer

Please note that the use of this actor and any data obtained through its use is at your own risk. The developer of this actor is not responsible for any consequences resulting from the use of this actor and the data it generates. It is your responsibility to ensure that you comply with all applicable laws and regulations governing the use of such data.