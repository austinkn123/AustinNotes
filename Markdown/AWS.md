## RUN ON AWS

- ATLAS Cloud is the Authoring and banking platform. It has a bunch of test questions and gets stored into different tests
- authoring - creating test questions
- banking - creating a test from authoring
- UTD captures HTML, saves answers, and displays the test to the user
- displays and how the user interacts with test
- no reporting
- uses a mongo db
- AWS is hosting ATLAS Cloud and UTD. They run in containers. AWS Services are used to run different functions on the data like save or view. The HTML files are stored in S3 buckets instead of a database
- aws - environment
  - files are usually stored with S3

all apps run in containers

- helps with framework versions
- so you dont have to install new dotnet 7 if the app had dotnet 6