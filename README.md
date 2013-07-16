A quick class I put together to access Google BigQuery data via query through Python.

1. Go to the [Google APIs console](https://code.google.com/apis/console) to create a new project. 
2. Services > BigQuery > status ON
3. API Access > "Create another client ID...". Choose "Service account" and click Create. 
4. Download your private keyfile.
5. Note down your service account's email address and project number (Overview > Project number).

Some example usage with Google ngrams:

	import easybigquery
	API = GoogleAPIFromServiceAccount(projectNumber, serviceEmail, pathToKeyfile)
	bq = GoogleBigQuery(API)

	def rawNgramData(word):
		query = "SELECT ngram, cell.volume_fraction FROM publicdata:samples.trigrams WHERE ngram CONTAINS '%s' GROUP BY ngram, cell.volume_fraction;" % word
		return bq.query(query)

	print rawNgramData("robot")