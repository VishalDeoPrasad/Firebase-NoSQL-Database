# Connect Firebase using Python
__Firebase__ real-time database is NoSQL(no sequral database) that allow developer is store and synchronize the data in real time.

Step 1: go to `https://firebase.google.com/`

Step 2: Click on `Get Started`
![alt text](image-1.png)

Step 3: click on `Create a Project`
![alt text](image-2.png)

Step 4: Give `Name of Project`
![alt text](image-3.png)
![alt text](image-4.png)
![alt text](image-5.png)
![alt text](image-6.png)

Step 5: Go to `Build` & Click on `Realtime database`
![alt text](image-7.png)

Step 6: `Create a database` for you project
![alt text](image-8.png)
![alt text](image-9.png)
`Locked mode`: Grant access to certain accounts. <br>
`Test Mode` : Grant access to anyone with the link can access the account.

![alt text](image-10.png)
`Database URL`: This means our database is ready to work. we are using this to access our database
![alt text](image-11.png)

__Note__: This is no sequeal database which mean there is no concept of `tables`, `keys` and `relationship`. Instead it is using json like object to store the data inside it called node. 
* Developer can create this node as key value pair. and store common data type like float, integer, string, list, & dictionary inside it.
![alt text](image-12.png)
![alt text](image-13.png)
`Each node has it's own path`
![alt text](image-14.png) <br>
Example
![alt text](image-15.png)

Step 7: `Install the firebase library` <br>
cmd: `pip install firebase_admin`

Step 8: `Go to project setting`
![alt text](image-16.png)
![alt text](image-17.png)

Step 9: `Save the file to you computer`

Step 10: Python code
```python
# import library
import firebase_admin
from firebase_admin import db, credentials
```

```python
#authenticate to firebase
url = "https://test-project-626e2-default-rtdb.asia-southeast1.firebasedatabase.app/"
cred = credentials.Certificate("credentials.json")
firebase_admin.initialize_app(cred, {"databaseURL" : url })
```

```python
# creating reference to root node
ref = db.reference("/")
```

```python
# retrieving data from root node
print(ref.get())
```

```python
print(db.reference("/videos").get())
```

```python
# set operation
db.reference("/videos").set(3)

# update operation (update existing value)
db.reference("/").update({"language":"python"})

# update operation (Add new key value)
db.reference("/").update({"subscribed": True})

# push operation
db.reference("/titles").push().set("Create modern UI in python")

# delete operation
db.reference("/language").delete()

# retrieving the data 
ref.get()
```

# Use Firebase features: 
Step 1: `Go to Console of firebase`
![alt text](image-18.png)
Step 2: `Create a project`
![alt text](image-19.png)
![alt text](image-20.png)
![alt text](image-21.png)
![alt text](image-22.png)
Note:`This is our project dashboard`
![alt text](image-23.png)

Step 3: Go to `Build` & Click on `Realtime database`
![alt text](image-7.png)

`Create a database for you project`
![alt text](image-8.png)
![alt text](image-9.png)
`Locked mode`: Grant access to certain accounts. <br>
`Test Mode` : Grant access to anyone with the link can access the account.

![alt text](image-10.png)
`Database URL`: This means our database is ready to work. we are using this to access our database
![alt text](image-11.png)

Step 4: `Add Firebase to your web app`
![alt text](image-24.png)
![alt text](image-25.png)

`Copy firebaseConfig dictionary and past it to our python file`
![alt text](image-26.png)
`This Crediential helps you to connect to the our project on firebase`

Step 5: Install Firebase library `pip install pyrebase4`
```python
import pyrebase
firebaseConfig = {
  'apiKey': "AIzaSyB_FuGMPWz4KQetXJsqE5ta-a8dlh_08u0",
  'authDomain': "test-project-626e2.firebaseapp.com",
  'databaseURL': "https://test-project-626e2-default-rtdb.asia-southeast1.firebasedatabase.app",
  'projectId': "test-project-626e2",
  'storageBucket': "test-project-626e2.appspot.com",
  'messagingSenderId': "829674087107",
  'appId': "1:829674087107:web:e52b04a7c3d33a143b7876",
  'measurementId': "G-VK007RC9FM"
}
#we are saying to pyrebase to initialize the app with given crediential
firebase = pyrebase.initialize_app(firebaseConfig)
```
## 1. Authentication: Loging in, Creating an account, Differnt types of user management
Step 1: `Use authentication feature`
![alt text](image-27.png)
![alt text](image-28.png)
![alt text](image-29.png)

Step 2: `Manually create a new user`
![alt text](image-30.png)
![alt text](image-31.png)

Step 3: `Sign in to you account`
```python
auth = firebase.auth()
email = input("Enter Your email")
password = input("Enter you password")
try:
    auth.sign_in_with_email_and_password(email, password)
    print("Success!")
except:
    print("Invalid user or password. Try again.")
```
Step 4: `Signup create a new user using command. Ask your Email and Password`
```python
# Create a new user
email = input("Enter Your email")
password = input("Enter you password")
confirm_password = input("Enter you password")

if password == confirm_password:
    try:
        auth.create_user_with_email_and_password(email, password)
        print("Success!")
    except:
        print("Email already exists")
```


## 2. Storage: Upload files on the internet as well as donwnload files in an internet.
Storage: `Storage is space on the croud use to store the data like images, audio, video, text, documentt etc` <br>
`it is just like a google drive just for you app.`
![alt text](image-32.png)
![alt text](image-33.png)
![alt text](image-34.png)
![alt text](image-35.png)
`create a bucket`
![alt text](image-36.png)
![alt text](image-37.png)
`Change the rule`: Now you can upload and download the files without any authentication.
![alt text](image-38.png)
`In case you are getting, Permission error` `Allow everyone to read and write into this storage`
![alt text](image-39.png)

#### Store a file on Firebase Storage
Python Code is use storage features
```python
firebaseConfig = {
  "apiKey": "AIzaSyBuhWUbRNVt651kvvS9uBl5t5FSdINxXas",
  "authDomain": "fir-course-9afa4.firebaseapp.com",
  "databaseURL": "https://fir-course-9afa4-default-rtdb.firebaseio.com",
  "projectId": "fir-course-9afa4",
  "storageBucket": "fir-course-9afa4.appspot.com",
  "messagingSenderId": "94327026554",
  "appId": "1:94327026554:web:9d2771939edeb475f15cc3",
  "measurementId": "G-6W970X59R3"
}
# this variable help us to interact the storage on the firebase
storage = firebase.storage()
```
## Upload
```python
file_name = input("Enter the name fo the file you want to upload")
cloud_file_name = input("Enter where you wanted to store the file")
storage.child(cloud_file_name).put(file_name)
```
![alt text](image-40.png)

## Get URL
```python
file_name = input("Enter the name fo the file you want to upload")
cloud_file_name = input("Enter where you wanted to store the file")
storage.child(cloud_file_name).put(file_name)
storage.child(cloud_file_name).get_url(None)
```
![alt text](image-42.png)

## Download 
```python
cloudfilename=input("Enter the name of the file you want to download")
storage.child(cloudfilename).download("", "download1.txt")
storage.child(cloud_file_name).get_url(None)
```


## 3. Firebase real-time database: Create, Read, Update and delete it

