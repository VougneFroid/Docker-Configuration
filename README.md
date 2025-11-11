# Instructions

## Building and uploading your image
1. Go to your app site where manage.py exist

2. enable your venv, then enter in terminal ``pip freeze > requirements.txt``

3. put the Dockerfiles, .dockerignore, and the docker-compose.yml on the same folder of your manage.py

4. Be sure to install docker in your system, ``docker --version`` on your terminal to check

5. build an image of your project with ``docker build -t ur-django-add:version`` note: you can replace 'version' anything like 'latest' or 'v1.0.0'

6. Login to Docker Hub to your terminal using ``docker login`` fill in credentials

7. Tag your image using ``docker tag <current-image-name> <dockerhub-username>/<image-name>:<version>``

    ex: docker tag my-app:v1.0.0 von/my-app:v1.0.0

8. Push your image using ``docker push <dockerhub-username>/<image-name>:<version>``

9. Verify your upload using this link https://hub.docker.com/r/yourusername/django-app


## Installing on another machine
1. Create a new folder for this activity then copy for_client\docker-compose.yml to the folder

2. Verify docker is installed to your system with ``docker --version`` 

3. Pull the image with ``docker pull yourusername/django-app:latest``

4. Be sure the docker-compose.yml is using image of your image

5. Start the app with ``docker-compose up -d``

6. Check the logs with ``docker-compose logs -f web``

7. You might see 0.0.0.0:8000, you can replace 0.0.0.0 with localhost or 127.0.0.1 and paste it to your browser

8. You can create a super user using ``docker-compose exec web python manage.py createsuperuser``


## Updating the image

### On Development Machine
1. Rebuild the image with ``docker-compose build``

2. Tag the build with new version ``docker tag <current-image-name> <dockerhub-username>/<image-name>:<new_version>``

    ex: docker tag my-app:v1.0.0 von/my-app:v1.0.1

3. Push the new version ``docker push my-app:v1.0.0 von/my-app:v1.0.1``

### On Target Machine
1. Pull the new version ``docker-compose pull``

2. Restart the image

    ``docker-compose down``

    ``docker-compose up -d``

3. Migrate ``docker-compose exec web python manage.py migrate``