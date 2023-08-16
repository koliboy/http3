# http3
HTTP3 is a custom JavaScript object that facilitates making HTTP requests using XMLHttpRequest, enabling web developers to interact with servers and fetch data from APIs. It provides a simplified interface for performing common HTTP methods such as GET and POST, along with features like progress tracking during uploads and downloads.

Here is a comprehensive description of the `http3` object:


# GET
2. `http3.get(request, data, options)`: A shortcut method for making GET requests using `http3.worker__`.

   Parameters:
   - `request` (string): The URL for the HTTP GET request.
   - `data` (object): Query parameters to be appended to the URL.
   - `options` (object): Additional options for the request.

   Example usage:
   ```javascript
   var req = http3.get('https://example.com/api/data', { param1: 'value1', param2: 'value2' });

   req.done(function(response) {
     console.log('GET request successful:', response);
   }).error(function() {
     console.log('Error occurred during the GET request.');
   });
   ```

Sure! Below is an example of how you can use the `http3.get()` method with various options to customize your GET request.

Assuming you have the `http3` object defined as provided in the previous code, here's how you can use the `http3.get()` method with different options:

```javascript
// Example usage of http3.get() with options
var apiUrl = 'https://api.example.com/data';

// Example of query parameters to be sent in the GET request
var queryParams = {
  category: 'electronics',
  sortBy: 'price',
  limit: 10,
};

// Define the options for the GET request
var options = {
  headers: {
    'Authorization': 'Bearer your_access_token', // Replace with your actual access token
    'User-Agent': 'Custom User Agent', // You can set a custom User-Agent header
  },
  responseType: 'json', // Parse the response as JSON
  status: 200, // Define the expected status code for successful responses
};

// Make the GET request using http3.get() with options
var request = http3.get(apiUrl, queryParams, options);

// Handling the response once the request is completed
request.done(function(responseData) {
  // `responseData` will contain the parsed JSON data from the response
  console.log('Response data:', responseData);
}).error(function() {
  console.log('Error occurred during the request.');
});

// Progress tracking (if needed)
request.downloadProgress(function(progress) {
  console.log('Download progress: ' + progress + '%');
});
```

In this example, we demonstrate how to use the `http3.get()` method with different options:

1. `queryParams`: We define an object `queryParams` to represent the query parameters to be sent along with the GET request. This object will be transformed into the URL's query string.

2. `options`: We define an object `options` to customize the request. The `options` object includes the following properties:
   - `headers`: An object containing custom headers to be sent with the request, such as an access token or a custom User-Agent.
   - `responseType`: Specifies the expected response type. In this case, we set it to `'json'`, indicating that we expect a JSON response that will be automatically parsed into an object.
   - `status`: Defines the expected status code for a successful response. In this example, we set it to `200`.

The `http3.get()` method is then used to make the GET request to the `apiUrl`, including the query parameters and options defined earlier. The response will be automatically parsed as JSON, and the `done()` callback will handle the parsed data. The `error()` callback will handle any errors that may occur during the request.

Please ensure that the actual API URL (`'https://api.example.com/data'` in this example) and the query parameters match your API's requirements. Additionally, customize the headers according to your specific use case and replace the `Authorization` header value with your actual access token.
   # POST

3. `http3.post(request, options)`: A shortcut method for making POST requests using `http3.worker__`.

   Parameters:
   - `request` (string): The URL for the HTTP POST request.
   - `options` (object): Additional options for the request, including the request body.

   Example usage:
   ```javascript
   var req = http3.post('https://example.com/api/data', {
     body: JSON.stringify({ key: 'value' }),
     headers: { 'Content-Type': 'application/json' }
   });

   req.done(function(response) {
     console.log('POST request successful:', response);
   }).error(function() {
     console.log('Error occurred during the POST request.');
   });
   ```

Please note that the provided code uses XMLHttpRequest, which is an older way of making HTTP requests in JavaScript. For modern web development, it is recommended to use Fetch API or Axios, which provide more powerful and convenient features for handling HTTP requests and responses.

# download

```javascript


// Function to trigger file download
function downloadFile() {
  var downloadLink = document.createElement('a');
  downloadLink.href = 'https://example.com/api/download'; // Replace with the URL to download the file
  downloadLink.target = '_blank'; // Open the link in a new tab
  downloadLink.download = 'file.txt'; // Specify the desired file name for download (e.g., file.txt)

  // Trigger the click event on the download link
  downloadLink.click();
}

// Function to handle file download progress
function handleDownloadProgress(progress) {
  console.log('Download progress: ' + progress + '%');

  if (progress === 100) {
    console.log('Download completed!');
  }
}

// Example usage: Call the downloadFile function when a button is clicked.
var downloadButton = document.getElementById('downloadButton');
downloadButton.addEventListener('click', function () {
  var req = http3.get('https://example.com/api/download', null, {
    responseType: 'blob', // Set the response type to 'blob' to handle binary data (file download)
  });

  // Progress callback to track the download progress
  req.downloadProgress(handleDownloadProgress);
});
```

In this example, we assume you have an HTML button element with the id "downloadButton." When the user clicks the "downloadButton," the `downloadFile` function is called.

The `downloadFile` function creates an anchor (`<a>`) element, sets its `href`, `target`, and `download` attributes, and then triggers a click event on the link. This effectively initiates the download process.

The download progress is tracked using the `req.downloadProgress` callback, which will be called with the current download progress percentage during the file download.

Please note that the actual download URL (`https://example.com/api/download` in this example) and the server's response headers must be configured correctly to allow the file download. Additionally, the server should correctly handle the download request and set the appropriate response headers for the file download.

Keep in mind that, as with the previous examples, the actual API URL and configuration may vary depending on your server's setup.

  // Progress callback to track the upload progress
  req.uploadProgress(function(progress) {
    console.log('Upload progress: ' + progress + '%');
  });

  // Handle the completion of the request
  req.done(function(response) {
    console.log('File uploaded successfully:', response);
  }).error(function() {
    console.log('Error occurred during the file upload.');
  });
}

// Example usage: Call the uploadFile function when a button is clicked.
var uploadButton = document.getElementById('uploadButton');
uploadButton.addEventListener('click', uploadFile);


# uploads-exmaple
Sure! I'll provide an example of how you can use the `http3` object to upload a file using FormData and monitor the progress during the upload.

Assuming you have the `http3` object defined as shown in the previous code:

```javascript


// Function to handle file upload
function uploadFile() {
  var fileInput = document.getElementById('fileInput');
  var file = fileInput.files[0];

  if (!file) {
    console.log('Please select a file.');
    return;
  }

  var formData = new FormData();
  formData.append('file', file);

  // Define the request using http3.post
  var req = http3.post('https://example.com/api/upload', {
    body: formData,
    headers: {
      // You might need to set appropriate headers based on your server's requirements.
      // For example, if you're uploading an image, you can set:
      // 'Content-Type': 'image/jpeg' for JPEG images or 'Content-Type': 'image/png' for PNG images.
      // Make sure to adjust the Content-Type according to the type of file you are uploading.
    },
  });

  // Progress callback to track the upload progress
  req.uploadProgress(function(progress) {
    console.log('Upload progress: ' + progress + '%');
  });

  // Handle the completion of the request
  req.done(function(response) {
    console.log('File uploaded successfully:', response);
  }).error(function() {
    console.log('Error occurred during the file upload.');
  });
}

// Example usage: Call the uploadFile function when a button is clicked.
var uploadButton = document.getElementById('uploadButton');
uploadButton.addEventListener('click', uploadFile);
```

In this example, we assume you have an HTML form with an input element of type "file" with the id "fileInput" and a button with the id "uploadButton." When the user selects a file using the file input and clicks the "uploadButton," the `uploadFile` function is called.

The `uploadFile` function reads the selected file, creates a FormData object, and then makes a POST request using `http3.post`. The upload progress is tracked using the `req.uploadProgress` callback, and the completion of the request is handled using the `req.done` and `req.error` callbacks.

Please note that the actual API URL and required headers may vary depending on your server's configuration. Make sure to adjust them accordingly. Additionally, handling file uploads and progress tracking on the server-side may require additional configuration and code on the server.

# response-type 
To use the `responseType: "json"` option with the `http3` object's `get()` method, you can do the following:

Assuming you have the `http3` object defined as provided in the code, you can now use the `get()` method with the `responseType: "json"` option to make a GET request that expects a JSON response. Here's an example:

```javascript
// Example usage of http3.get() with responseType: "json"
var apiUrl = 'https://api.example.com/data';

var request = http3.get(apiUrl, null, {
  responseType: 'json',
});

// Handling the response once the request is completed
request.done(function(responseData) {
  // `responseData` will be the parsed JSON data from the response
  console.log('Response data:', responseData);

  // You can access individual properties from the JSON data, for example:
  console.log('Value of "property1":', responseData.property1);
}).error(function() {
  console.log('Error occurred during the request.');
});

// Progress tracking (if needed)
request.downloadProgress(function(progress) {
  console.log('Download progress: ' + progress + '%');
});
```

In this example, the `http3.get()` method is used to make a GET request to the `apiUrl`, which should return a JSON response. By passing the `responseType: 'json'` option, the XMLHttpRequest object will automatically parse the response data as JSON. This means that the `responseData` parameter in the `done()` callback will already be an object containing the parsed JSON data.

Please note that when using `responseType: 'json'`, the HTTP response's `Content-Type` header must indicate that the response is in JSON format. Otherwise, the parsing may fail, and the `done()` callback might not be triggered.

Keep in mind that this example assumes that the server will respond with a valid JSON object. If the response is not valid JSON or if there are network issues, the `error()` callback will be triggered.

 # formdata
 Sure! I'll provide an example of an HTML `<form>` and how you can use the `http3` object to submit the form data using FormData through a POST request.

HTML Form:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Form Data Example</title>
</head>
<body>
    <h2>Submit Form Data</h2>
    <form id="myForm">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required><br>

        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required><br>

        <label for="message">Message:</label><br>
        <textarea id="message" name="message" rows="4" required></textarea><br>

        <button type="submit">Submit</button>
    </form>

    <script src="http3.js"></script>
    <script src="app.js"></script>
</body>
</html>
```

JavaScript (app.js):
```javascript
// Assuming you have the `http3` object defined as provided in the previous code.

document.getElementById('myForm').addEventListener('submit', function (event) {
    event.preventDefault(); // Prevent the form from submitting the traditional way.

    // Get the form data using FormData
    var formData = new FormData(event.target);

    // Define the request using http3.post
    var req = http3.post('https://example.com/api/submit', {
        body: formData,
    });

    // Handling the response once the request is completed
    req.done(function(responseData) {
        console.log('Response data:', responseData);
    }).error(function() {
        console.log('Error occurred during the request.');
    });

    // Progress tracking (if needed)
    req.uploadProgress(function(progress) {
        console.log('Upload progress: ' + progress + '%');
    });
});
```

In this example, we have an HTML `<form>` with three fields: Name, Email, and Message. The form's `submit` event is captured in the JavaScript file (app.js) using the `addEventListener` method. We prevent the default form submission behavior (page refresh) with `event.preventDefault()` to handle the form submission asynchronously.

When the user clicks the "Submit" button, the form data is gathered using the FormData object, which automatically collects the form's field data. We then create a POST request using `http3.post()`, passing the FormData object as the request body.

The `done()` callback handles the response once the request is completed successfully, and the `error()` callback handles any errors that may occur during the request.

The `uploadProgress()` callback is used to track the progress of the file upload if the server expects a file upload or if you have specific processing needs during the upload.

Please note that you need to replace `'https://example.com/api/submit'` with the actual API endpoint URL that will handle the form submission on your server. Also, ensure that your server handles the POST request correctly and returns an appropriate response. Additionally, adjust the Content-Type and other headers if necessary, based on your server's requirements.

# UPLOAD-rate
The provided code does not directly show a way to measure the total amount of data sent per second. However, if you want to calculate the total data sent per second during an upload, you can utilize the upload progress information that's being tracked in the `uploadProgress` function. The progress value is a percentage indicating how much of the data has been uploaded.

To calculate the total data sent per second, you can use the following steps:

1. Keep track of the current progress value and the time elapsed.
2. Calculate the difference in progress values over time to determine the change in the amount of uploaded data.
3. Divide the change in data by the time difference to get the upload rate in percentage per second.

Here's a modified version of the example code to help you achieve this:

```javascript
document.addEventListener('DOMContentLoaded', function () {
    const uploadForm = document.getElementById('uploadForm');
    const fileInput = document.getElementById('fileInput');
    const uploadButton = document.getElementById('uploadButton');
    let lastProgress = 0;
    let lastTime = Date.now();

    uploadButton.addEventListener('click', function () {
        const file = fileInput.files[0];
        if (file) {
            const formData = new FormData();
            formData.append('file', file);

            // Options for the POST request
            const options = {
                responseType: 'json', // You can customize this
                headers: {
                    // You can add additional headers here
                }
            };

            const request = http3.post('/upload', options)
                .done(function (response) {
                    console.log('Upload successful:', response);
                })
                .error(function () {
                    console.log('Upload failed');
                });

            request.uploadProgress(function (progress) {
                const currentTime = Date.now();
                const timeDifference = (currentTime - lastTime) / 1000; // Convert to seconds
                const dataChange = (progress - lastProgress) / 100 * file.size; // Convert progress to data size
                const uploadRate = dataChange / timeDifference;
                
                console.log('Upload progress:', progress, '%');
                console.log('Data sent per second:', uploadRate.toFixed(2), 'bytes/s');

                // Update last progress and time
                lastProgress = progress;
                lastTime = currentTime;
            });

            request.timeOut(10000, function () {
                console.log('Upload timed out');
            });

            // Send the FormData as the request body
            options.body = formData;
            request.send(options);
        }
    });
});
```

Please note that this approach provides an estimate of the upload rate in bytes per second. Keep in mind that network conditions, server responsiveness, and other factors can affect the accuracy of this calculation.
