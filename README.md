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
