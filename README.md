# Pentaho Data Integration (aka Kettle) Analytics transformations

## organic-search-terms.ktr

Pulls a report of organic search terms and outputs them to csv file

Kettle Properties to set in the kettle.properties file (or through the GUI: Edit > Edit kettle.properties file)

```
CUSTOM_GOOGLE_ANALYTICS_API_KEY
CUSTOM_GOOGLE_ANALYTICS_EMAIL
CUSTOM_GOOGLE_ANALYTICS_PASSWORD
```

## organic-search-terms-categorize.ktr

Contains a step that categorizes the search terms based on regular expressions

The step roughly looks like so and adds `category` and `match` columns to the csv output

```
category = ''; 
match = ''; // captures the regex that caused the match

regexes = {
  'police': /police|crime|\bpd\b/,
  'jail': /jail|inmate|detention/
}

categories = Object.keys(regexes);

for (var i = 0; i < categories.length; i++) {
  potentialCategory = categories[i];
  regex = regexes[potentialCategory];
  matches = [];
  if (matches = keyword.match(regex)) {
    match = matches[0];
    category = potentialCategory;
  }
}
```
