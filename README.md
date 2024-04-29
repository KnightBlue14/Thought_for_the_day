# Thought for the Day API
A personal project based on Warhammer 40,000's 'Thought for the day', a series of quotes and phrases that appear throughout works from the franchise. This project takes a collection of quotes, then publishes them via an API. It can be run as found in this repository, or via a Docker container
## Description
The project covers the extraction of individual quotes from the Warhammer fansite Lexicanum, then the importing of the quotes into a Flask API that can readily be accessed. The idea was that the ouptut could be used in conjunction with a reciever, such as an internet-of-things device (i.e. a Raspberry Pi), to display a quote on a regular schedule.

## Technologies used
* Python - Python was used as the backbone of the project, for webscraping and creating the application. Flask is used as the foundation of the application, but the actual programming is based in Python. Optionally, Docker can also be used to host the application , but is not required
## How to use

### App.py
This file contains the settings for the application. As it is, it includes two endpoints, a homepage to confirm that the app is running, and the page for the posting of quotes. If you wish to add any more, simply add a block beginning with '@app.get("/{endpoint_name}")', then write a function for what you want to appear at the endpoint.

### ThoughtfortheDay.py
This is the script that webscrapes the three pages on Lexicanum for the quotes used, which can be found here (https://wh40k.lexicanum.com/wiki/Thought_for_the_day). There is a large block of if statements, covering additional information that is not needed, mostly sources and admin information that use the same element type as the quotes. There is also another block that tries to print the quote, then adds it to a list if successful, which is needed as some quotes featured characters that python was unable to print, and would break the application.

### thought_for_the_day.csv
The collection of quotes used in the app. Even after the filters mentioned in the script, some editing was still needed, so if you redownload them be sure to check for any broken or misplaced lines.

If you are not interested in Docker, these are all you need. Just place the files in a directory, create a virtual environment, install flask WITHIN the environment, then use the command 'flask run' (or 'python -m flask run'). If you are, you will aslo need the following files -
### requirements.txt
The needed modules for the app, covering flask and it's dependencies

### Dockerfile
The blueprint for your container. This can be left alone, unless you change the default port used by your flask application, in which case you will need to change EXPOSE from 5000 to your port. Other than that, just have everything in the same folder, use the command - 
```
docker build -t {image-name} .
```
If everything is properly configured, it will then build the container. From there, using Docker Desktop, run the image. Under 'Optional settings', you will need to select a port so that your machine can access the container (i.e. 5005).
