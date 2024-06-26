1. cd C:\\Program Files\\PostgreSQL\\15\\data
2. open pg_hba.conf in text editor
3. change 
	host    all    all    trust 
4. restart service
	1. GUI
		1. Win + R
		2. type services.msc 
		   ![[Pasted image 20240626082711.png]]
		3. stop the service
		4. start
	2. cmd
		1. net stop postgresql-x64-version
		2. net start postgresql-x64-version
#pgadmin4 