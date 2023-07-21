# http3
HTTP3 is a custom JavaScript object that facilitates making HTTP requests using XMLHttpRequest, enabling web developers to interact with servers and fetch data from APIs. It provides a simplified interface for performing common HTTP methods such as GET and POST, along with features like progress tracking during uploads and downloads.

Here is a comprehensive description of the `http3` object:

**1. Core Method: `worker__(type, request, data, options)`**
   - This method is the foundation of HTTP3 and is responsible for making HTTP requests.
   - Parameters:
     - `type` (string): The HTTP method type, either 'GET' or 'POST'.
     - `request` (string): The URL for the HTTP request.
     - `data` (object): The data to be sent in the request (used in POST requests).
     - `options` (object): Additional options for the request, like headers, response type, etc.
   - Returns: An object (`data_return`) that allows chaining various callbacks to handle request completion, errors, and progress tracking.

**2. Shortcut Methods: `get(request, data, options)` and `post(request, options)`**
   - These are convenience methods that use `worker__` under the hood to perform GET and POST requests, respectively.
   - `get()` is used for GET requests, and `post()` is used for POST requests.
   - They provide a simpler way to initiate common HTTP methods without directly calling `worker__`.

**3. Progress Tracking: `uploadProgress(func)` and `downloadProgress(func)`**
   - These methods enable tracking the progress of uploads and downloads, respectively.
   - The `uploadProgress` method is used to track the progress of file uploads.
   - The `downloadProgress` method is used to track the progress of file downloads.
   - Progress is represented as a percentage (0-100), and the provided callback function is called with the current progress value.

**4. Response Handling: `done(func)` and `error(func)`**
   - These methods allow handling the response once the request is completed.
   - The `done` method is used when the request is successful (status code matches options.status).
   - The `error` method is used when the request encounters an error (status code differs from options.status).
   - The provided callback functions are called with the response data or error handling logic.

**5. Additional Functionality**
   - `timeOut(time, func)`: Sets a timeout for the request and calls the provided function if the request exceeds the specified time.
   - `abort(func)`: Aborts the request and calls the provided function when the request is aborted.

**6. Usage**
   - Developers can use the `http3` object to initiate HTTP requests and handle responses in a more streamlined manner.
   - It supports both simple requests with predefined methods (`get` and `post`) and complex requests with custom options (`worker__`).
   - The object simplifies handling asynchronous behavior and provides built-in progress tracking during uploads and downloads.
   - Developers can chain multiple callbacks to handle different aspects of the request and response flow.

Please note that while the `http3` object provides a basic way to make HTTP requests, modern web development often utilizes more sophisticated libraries like Axios or Fetch API due to their broader feature sets, better support for modern browser standards, and improved error handling capabilities.


The provided code defines an HTTP3 object with methods for making HTTP requests using XMLHttpRequest. The object has three main methods: `worker__`, `get`, and `post`. The `get` and `post` methods are simply shortcuts to the `worker__` method, with the appropriate HTTP method (GET or POST) predefined.

Below is a description of the methods available in the HTTP3 object:

1. `http3.worker__(type, request, data, options)`: This method is the core function responsible for making HTTP requests. It supports both GET and POST methods and includes various options to configure the request. The method returns an object (`data_return`) that allows chaining different callbacks.

   Parameters:
   - `type` (string): The HTTP method type, either 'GET' or 'POST'.
   - `request` (string): The URL for the HTTP request.
   - `data` (object): The data to be sent in the request (used in POST requests).
   - `options` (object): Additional options for the request, such as headers, response type, etc.

   Example usage:
   ```javascript
   var req = http3.worker__('GET', 'https://example.com/api/data', null, {
     headers: { 'Authorization': 'Bearer your_access_token' },
     responseType: 'json',
   });

   req.done(function(response) {
     console.log('Request successful:', response);
   }).error(function() {
     console.log('Error occurred during the request.');
   });
   ```

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


var http3 = { /* ... The previously defined http3 object ... */ };

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

  Certainly! Below is an example of how you can use the `http3` object to download a file and monitor the download progress.

Assuming you have the `http3` object defined as shown in the previous code:

```javascript
var http3 = { /* ... The previously defined http3 object ... */ };

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
