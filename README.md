# Json
Here is a comprehensive list of CLI commands and techniques for working with JSON data

### **JSON CLI Commands and Techniques**

#### **1. Basic JSON Operations**

- **Pretty-print JSON:**
  ```sh
  cat file.json | jq .
  ```

- **Read a JSON file:**
  ```sh
  jq '.' file.json
  ```

- **Filter JSON data:**
  ```sh
  jq '.key' file.json
  ```

- **Extract a nested value:**
  ```sh
  jq '.key.nestedKey' file.json
  ```

- **Extract multiple keys:**
  ```sh
  jq '{key1: .key1, key2: .key2}' file.json
  ```

#### **2. jq Advanced Techniques**

- **Modify JSON data:**
  ```sh
  jq '.key = "newValue"' file.json
  ```

- **Add a new key-value pair:**
  ```sh
  jq '. + {"newKey": "newValue"}' file.json
  ```

- **Delete a key:**
  ```sh
  jq 'del(.key)' file.json
  ```

- **Iterate over an array:**
  ```sh
  jq '.arrayName[]' file.json
  ```

- **Select elements based on condition:**
  ```sh
  jq '.arrayName[] | select(.key == "value")' file.json
  ```

- **Group by a specific key:**
  ```sh
  jq 'group_by(.key) | map({key: .[0].key, values: .})' file.json
  ```

#### **3. JSON Manipulation with Python**

- **Read and parse JSON file:**
  ```python
  import json

  with open('file.json') as f:
      data = json.load(f)
  ```

- **Modify JSON data:**
  ```python
  data['key'] = 'newValue'
  ```

- **Write JSON to file:**
  ```python
  with open('file.json', 'w') as f:
      json.dump(data, f, indent=4)
  ```

- **Convert JSON to Python object:**
  ```python
  json_string = '{"key": "value"}'
  data = json.loads(json_string)
  ```

- **Convert Python object to JSON:**
  ```python
  json_string = json.dumps(data, indent=4)
  ```

#### **4. JSON Validation**

- **Validate JSON file:**
  ```sh
  jq empty file.json
  ```

- **Using Python for validation:**
  ```python
  import json

  try:
      with open('file.json') as f:
          data = json.load(f)
      print("Valid JSON")
  except ValueError as e:
      print("Invalid JSON: ", e)
  ```

- **Using `jsonlint` for validation:**
  ```sh
  jsonlint file.json
  ```

#### **5. JSON Data Transformation**

- **Flatten nested JSON:**
  ```sh
  jq 'flatten' file.json
  ```

- **Merge two JSON objects:**
  ```sh
  jq -s '.[0] * .[1]' file1.json file2.json
  ```

- **Convert JSON to CSV:**
  ```sh
  jq -r '[.[] | {key1, key2}] | (first | keys_unsorted) as $keys | $keys, map([.[ $keys[] ]])[] | @csv' file.json
  ```

- **Convert CSV to JSON:**
  ```sh
  csvtojson file.csv > file.json
  ```

#### **6. Querying JSON with `jq`**

- **Count elements in an array:**
  ```sh
  jq '.arrayName | length' file.json
  ```

- **Sum values in an array:**
  ```sh
  jq '[.arrayName[].key] | add' file.json
  ```

- **Find maximum value in an array:**
  ```sh
  jq 'max_by(.key) | .key' file.json
  ```

- **Sort an array by a key:**
  ```sh
  jq 'sort_by(.key)' file.json
  ```

#### **7. JSON Operations in Bash**

- **Filter JSON data in bash:**
  ```sh
  curl -s 'https://api.example.com/data' | jq '.key'
  ```

- **Assign JSON value to a variable:**
  ```sh
  value=$(jq -r '.key' file.json)
  ```

- **Loop through JSON array:**
  ```sh
  for item in $(jq -r '.arrayName[] | @base64' file.json); do
    _jq() {
      echo ${item} | base64 --decode | jq -r ${1}
    }
    echo $(_jq '.key')
  done
  ```

#### **8. Integrating JSON with Other Tools**

- **Extract and pass JSON data to another command:**
  ```sh
  value=$(jq -r '.key' file.json)
  echo $value | another_command
  ```

- **Use JSON data in shell scripts:**
  ```sh
  #!/bin/bash
  data=$(jq -r '.key' file.json)
  echo "The value of key is: $data"
  ```

- **Combine JSON with `curl` for API requests:**
  ```sh
  curl -s 'https://api.example.com/data' -H "Content-Type: application/json" -d '{"key": "value"}' | jq '.'
  ```

- **Filter and manipulate JSON from HTTP responses:**
  ```sh
  curl -s 'https://api.example.com/data' | jq '.results[] | select(.key == "value")'
  ```

This extensive list covers a broad range of JSON CLI commands, including basic operations, advanced techniques with `jq`, Python scripts for JSON manipulation, validation methods, data transformation, querying, and integration with other tools. These commands should provide a solid foundation for working with JSON in various environments.
