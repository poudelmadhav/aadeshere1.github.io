---
layout: post
title: Fix garble in CSV when generating with ruby
date: 2024-12-19
---

Using ruby to create CSV is quite straightforward process. There’s generate method that can generate the CSV which can be directly sent over HTTP to be downloaded by user.

Most of the application that can read CSV file can read the generated CSV without any problem, however when we try to open the CSV that contain Japanese characters with Microsoft Excel, it will show garbled text.

Below is the sample code to generate CSV

```
def send_csv_data
  output_csv = CSV.generate(encoding: 'UTF-8', headers: true) do |csv|
    headers = [...]
    csv << headers
    values = return_from_some_method
    csv << values
    end
  end

  send_data output_csv, filename: "random-name.csv"
end
```

‌

To fix the garbled text and make excel understand to treat it as UTF-8 with bom, we need to add an unicode character.

‌

```
def send_csv_data

  # NOTE: for excel to recognize the csv as UTF-8 with BOM
  bom = "\uFEFF"

  output_csv = CSV.generate(encoding: 'UTF-8', headers: true) do |csv|
  ...
  end

  send_data bom + output_csv, filename: "random-name.csv"
end
```
        