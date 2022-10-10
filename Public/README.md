## Steps to follow in the terminal

# 1. Build dba Dockerfile from dba terminal location
docker build -t my_dba .

# 2. Build db Dockerfile from db terminal location
docker build -t my_db .

# 3. Run dba Dockerfile from db terminal location
docker run --name mydba --network mynetwork -p 8081:80 -d my_dba

# 4. Run db Dockerfile from db terminal location
docker run --name mydb --network mynetwork -itd -p 5432:5432 -d my_db

# 5. Enter the Public Dockerfile location for building my_django
docker build -t my_django .

# 6. Run my_django from Public terminal location
docker run -it -p8000:8000 --network mynetwork -v "$(pwd)/app:/app" my_django /bin/bash

# 7. In settings.py, we have changed the database entries depening on our user = root, password = pass, host = mydb, name = web, port = 5432

# 8. After saving the above, we migrate
root@fcbb5da5d62a:/app# python /app/app/manage.py migrate

# 9. Create superuser
root@fcbb5da5d62a:/app# python /app/app/manage.py createsuperuser
Username (leave blank to use 'root'): 
Email address: a@a.com
Password: pass
Password (again): pass

# 10. Run server
root@fcbb5da5d62a:/app# python /app/app/manage.py runserver 0.0.0.0:8000

# 11. Open http://localhost:8081/browser/ and enter the server details name: mydb, root, pass

# 12. Open http://localhost:8000/admin/ and enter the user : root , password : pass

# 13. In the pgadmin, we should be able to view the tables created under the schemas in web.