## Uploading Videos to S3

### Step 1 - Create a Bucket

In the IAM console:

Click services in the top left corner.
Scroll down to storage and select S3 from the right-hand list.
Click "Create bucket" and give it a name.
You can choose any region you want. Leave the rest of the settings and click "Create bucket" once more.

If you want people to access your bucket ensure you untick where it says block all public access.


![progetass3interface-aws-createbucket](https://user-images.githubusercontent.com/106158041/205350520-72411614-69d3-4dd9-bf07-c7e10b0b522c.png)

### Step 2 - Upload your files

You can do in various different ways, for Python.

- run this command `pip install boto3`

Then you upload files into S3 using Python

```
import boto3
s3.upload_file(
    Filename="data/downloaded_from_s3.csv",
    Bucket="sample-bucket-1801",
    Key="new_file.csv",
)
```
or

```
import boto3
from botocore.exceptions import NoCredentialsError

def upload_to_aws(local_file, bucket, s3_file):
    s3 = boto3.client('s3', aws_access_key_id=ACCESS_KEY,
                      aws_secret_access_key=SECRET_KEY)

    try:
        s3.upload_file(local_file, bucket, s3_file)
        print("Upload Successful")
        return True
    except FileNotFoundError:
        print("The file was not found")
        return False
    except NoCredentialsError:
        print("Credentials not available")
        return False


uploaded = upload_to_aws('local_file', 'bucket_name', 's3_file_name')
```
Alternatively if you want to use JavaScript you can use this function

```
<script type="text/javascript">
function s3upload() {
   var files = document.getElementById('fileUpload').files;
   if (files) 
   {
     var file = files[0];
     var fileName = file.name;
     var filePath = 'my-first-bucket-path/' + fileName;
     var fileUrl = 'https://' + bucketRegion + '.amazonaws.com/my-    first-bucket/' +  filePath;
     s3.upload({
        Key: filePath,
        Body: file,
        ACL: 'public-read'
        }, function(err, data) {
        if(err) {
        reject('error');
        }
        alert('Successfully Uploaded!');
        }).on('httpUploadProgress', function (progress) {
        var uploaded = parseInt((progress.loaded * 100) / progress.total);
        $("progress").attr('value', uploaded);
      });
   }
};
</script>
```
