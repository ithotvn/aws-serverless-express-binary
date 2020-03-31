# AWS Serverless Express

Customized from `https://github.com/awslabs/aws-serverless-express`. This supported image upload via node server like NestJS, etc...

## Getting Started

Check details at: https://github.com/awslabs/aws-serverless-express

```bash
npm install aws-serverless-express-binary
```

## Sample

```
req.on("data", function(chunk) {
  data.push(chunk);
})
.on("end", function() {
  body = Buffer.concat(data).toString();
  var bb = new busboy({ headers: { 'content-type': contentType } });

  bb.on('file', function (fieldname, file, filename, encoding, mimetype) {
    const mimeType = mimetype;
    const ext = filename.split('.')[1];
    let chunks;
    file.on('data', function (data) {
      chunks = data;
    }).on('end', function () {
      let base64Image = new Buffer(chunks.toString(), 'binary').toString('base64');
      const fileData = new Buffer(base64Image, 'base64');
    });
  })

  bb.end(body);
```