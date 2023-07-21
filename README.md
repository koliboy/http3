# http3
HTTP3 is a custom JavaScript object that facilitates making HTTP requests using XMLHttpRequest, enabling web developers to interact with servers and fetch data from APIs. It provides a simplified interface for performing common HTTP methods such as GET and POST, along with features like progress tracking during uploads and downloads.

Here is a comprehensive description of the `http3` object:



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
