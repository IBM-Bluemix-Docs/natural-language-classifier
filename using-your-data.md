---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Data preparation
After you create, train, and query an {{site.data.keyword.nlclassifierfull}} with the data in the [Getting started](/docs/services/natural-language-classifier/getting-started.html) example, you will want to create a classifier that works with your own data. You assemble and provide this training data.
{:shortdesc}

## Structure of training data
{: #training-structure}

You can provide the data to train the {{site.data.keyword.nlclassifiershort}} in comma-separated value (CSV) format.

In the CSV format, a row in the file represents an example record. Each record has two or more columns. The first column is the representative text to classify. The additional columns are classes that apply to that text. The following image shows a CSV file that has four records. Each record in this sample includes the text input and one class, which are separated by a comma:

![](images/train_sample.png)

This example is a small sample. Proper training data includes many more records.

Download the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> file to see a sample training data file.

### Additional metadata
{: #additional-metadata}

In addition to the text and classes, the request to create a classifier includes additional information. The metadata identifies the language of the data, and you can also include a name to help you identify the classifier.

### CSV training data file format
{: #csv-file-format}

Make sure that your CSV training data adheres to the following format requirements:

- The data must be UTF-8 encoded.
- Separate text values and each class value by a comma delimiter. Each record (row) is terminated by an end-of-line character, which is a special character or sequence of characters that indicate the end of a line.
- Each record must have one text value and at least one class value.
- Class values cannot include tabs or end-of-line characters.
- Text values cannot contain tabs or new lines without special handling. To preserve tabs or new lines, escape a tab with `\t`, and escape new lines with `\r`, `\n` or `\r\n`.

    For example, `Example text\twith a tab` is valid, but <code>Example text&nbsp;&nbsp;&nbsp;&nbsp;with a tab</code> is not valid.
- Always enclose text or class values with double quotation marks in the training data when it includes the following characters:
    - Commas: `"Example text, with comma"`.
    - Double quotation marks. In addition, quotation marks must be escaped with double quotation marks: `"Example text with ""quotation"""`.

## Size limitations
{: #training-limits}

There are both minimum and maximum limits to the training data:

- The training data must have at least five records (rows), no more than 20,000 records, and no more than 3,000 classes.
- The maximum total length of a text value is 1024 characters.
