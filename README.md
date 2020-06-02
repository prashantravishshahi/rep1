#### JSON To CSV Converter
This code converts JSON to CSV.

#### Usage:

1 - Using a JSON String:

- JSON string:
```json
{
	"firstName": "Prashant",
	"lastName": "Shahi"
}
```

- JAVA code:
```java
/*
 * Parse a JSON String and convert it to CSV
 */
List<Map<String, String>> flatJson = JSONFlattener.parseJson(jsonString);
// Using the default separator ','
// If you want to use an other separator like ';' or '\t' use
// CSVWriter.getCSV(flatJSON, separator) method
CSVWriter.writeToFile(CSVWriter.getCSV(flatJson), "files/sample_string.csv");
```

- CSV output:
```csv
lastName,firstname
Shahi,Prashant
```
2 - Using a JSON file:

- JSON file:

considering the file `simple.json` in `/files` directory, contains the following JSON
```json
[
    {
        "studentName": "Foo",
        "Age": "12",
        "subjects": [
            {
                "name": "English",
                "marks": "40"
            },
            {
                "name": "History",
                "marks": "50"
            }
        ]
    },
    {
        "studentName": "Bar",
        "Age": "12",
        "subjects": [
            {
                "name": "English",
                "marks": "40"
            },
            {
                "name": "History",
                "marks": "50"
            },
            {
                "name": "Science",
                "marks": "40"
            }
        ]
    },
    {
        "studentName": "Baz",
        "Age": "12",
        "subjects": []
    }
]
```

- JAVA code:
```java
/*
 *  Parse a JSON File and convert it to CSV
 */
// There is 2 methods to parse the JSON file
// 1- JSONFlattener#parseJson(File file):
//    This will use the default encoding UTF-8 to parse the given file.
// 2- JSONFlattener#parseJson(File file, String encoding):
//    This will parse the file using the specified character encoding.
flatJson = JSONFlattener.parseJson(new File("files/simple.json"), "UTF-8");
// Using ';' as separator
CSVWriter.writeToFile(CSVWriter.getCSV(flatJson, ";"), "files/sample_file.csv");
```
```csv
Age;subjects[1].marks;subjects[1].name;subjects[2].marks;subjects[2].name;studentName;subjects[3].marks;subjects[3].name
12;40;English;50;History;Foo;;
12;40;English;50;History;Bar;40;Science
12;;;;;Baz;;
```

3 - Using a JSON returned from a URL:

- JAVA code:
```java
/*
 *  Parse JSON from URL and convert it to CSV
 */
// There is 2 methods to parse a JSON returned from a URI
// 1- JSONFlattener#parseJson(URI uri):
//    This will use the default encoding UTF-8 to parse the JSON returned from the given uri.
// 2- JSONFlattener#parseJson(URI uri, String encoding):
//    This will parse the JSON returned from the uri using the specified character encoding.
flatJson = JSONFlattener.parseJson(new URI("http://echo.jsontest.com/firstname/Brahim/lastName/Arkni"));
// Using '\t' as separator
CSVWriter.writeToFile(CSVWriter.getCSV(flatJson, "\t"), "files/sample_uri.csv");
```

- JSON:

for this example, I used the web service [echo.jsontest.com](http://echo.jsontest.com) to echo a JSON object like the following
```json
{
	"firstName": "Prashant",
	"lastName": "Shahi"
}
```

- CSV output 
```csv
lastName	firstname
Shahi		Prashant
```

