# Starter project  
Django starter project with postgres or mysql.  
The project is dockeriezed using docker-compose.  
To start the project run `docker-compose up -d` and it will start the django and postgres containers.  
To change to the mysql container, uncomment the service in the docker-compose file and change the environment variables in the env_variables/django.env file.  

This project is not ment to be a production-ready. Use it only for development or/and make the proper modifications before using it in a production environment