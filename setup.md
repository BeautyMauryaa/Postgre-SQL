# setup:
1. install posgresql 
- update package sudo apt update
- install postgresql sudo apt install postgresql postgresql-contrib

2. check
- sudo systemctl status postgresql -> Active: active (running)
- sudo systemctl start postgresql
- sudo systemctl enable postgresql 

3. check psql
- psql --version

4. install pgadmin





# understand posgresql server
- it create user called postgres
- we can access postgresql through sudo -u postgres psql 
postgres=# ( inside the postgresql)