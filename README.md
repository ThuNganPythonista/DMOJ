# DMOJ : An algorithmic problem-solving platform #

# I share the instructions to set up `site` and `the judge` of an open source code DMOJ #

**OFFICAL INSTRUCTIONS OF DMOJ : https://docs.dmoj.ca/#/site/installation **


Chapter 1 :  Set Up “Site”
Chapter 2 : Set Up “Judge Server”

I) Set up prerequisites :

Prerequisites include software, libraries, or configurations to help us avoid conflicts during the process of deploying and enhance the security of the environment, resulting in stable status.
(*1)
`brew update`  : Homebrew stores all its packages in its main repository. We `update` its latest software packages when there are updates and changes. Similarly, we use `apt update` command for Ubuntu.
(*2)
`brew install git gcc make python3 libxml2 libxslt zlib gettext curl redis ` :

It means that we will install all of these software packages :
git: Manage changes in open source code.
gcc:  C and C++ compiler
make: A tool to help you automate everything like our installation process of software.
python3:  version 3 of Python.
libxml2: software library XML.
libxslt: XSLT library
zlib: library for data compression.
gettext: a library supports program with multi-language (l10n) and internationalisation (i18n)
curl: A computer program like a command-line tool for transmitting and acquiring data using several network protocols.
redis: In-memory key-value database system.
With Ubuntu, we change `brew` into `apt`
(*3)
`curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -` :

Let’s break down each of components with us :
	
curl : this one, we already installed in the previous command. It will make HTTP requests. 
-sL : You can look it up in this list (https://gist.github.com/eneko/dc2d8edd9a4b25c5b0725dd123f98b10)
Yes, it is one of the flags of curl option
`https://deb.nodesource.com/setup_18.x` : Setup NodeJs18
|: Pipe shell command
sudo -E bash - : This is a command in the system of Unix/Linux. In this case, It is used to install Node.js from NodeSource on Debian-based systems.

For macOs, we run different commands to set up nodeJs18 :

	`brew services start redis`
`brew install node@18`
`export LDFLAGS="-L/usr/local/opt/node@18/lib`
`export CPPFLAGS="-I/usr/local/opt/node@18/include`
	
This command sequence conducts this process : start the Redis service, install NodeJs18 via Homebrew and set up environment variables 


	(*4)sudo npm install -g sass postcss-cli postcss autoprefixer

Let’s break down each of components with us :
	
sudo : It stands for "superuser do", and here we run `sudo` for installing npm packages.
npm : Node Package Manager, a package manager for JavaScript programming language
install : install is install :vv
-g : to make sure  your packages should be install globally in the system
sass, postcss-cli, postcss and autoprefixer : the different kinds of css properties 


For Ubuntu,  we can perform similarly by the command : 
`npm install -g sass postcss-cli postcss autoprefixer`
 
II) Create databases:

Update the latest MariaDB version

(*5) `brew update` : update available packages through HomeBrew
(*6)` brew install mariadb` : Set up MariaDb, manage open source code database
(*7) `brew services start mariadb` : The previous command, we already installed MariaDb, so this command is to run and start to work with the database.
(*8) `brew install mysql-client` : We may be familiar with the concept of MySQL Client If we are used to learning, MySQL. Mysql-client allows users to interact directly with the database.  Here, it helps us interact with the MySQL and MariaDB database.

(*9) echo 'export PATH="/usr/local/opt/mysql-client/bin:$PATH"' >> ~/.zshrc
 (*10) export LDFLAGS="-L/usr/local/opt/mysql-client/lib"
(*11) export CPPFLAGS="-I/usr/local/opt/mysql-client/include"

=> It's all around MySQL Client. It make sure our system locate exactly MySQL Client libraries and headers, including 
Update the PATH
Setting LDFLAGS
Setting CPPFLAGS

Next, we access to mysql to create essential databases and user

(*12)
`sudo mysql` : We all know about `superuser` that is system administration, so we launch mysql client command as superuser for performing tasks related to privileges and administration, including modifying databases, users, or configurations.

after that, our terminal indicates  : `mariadb>` to set up database
(*13)
mariadb> CREATE DATABASE dmoj DEFAULT CHARACTER SET utf8mb4 DEFAULT COLLATE utf8mb4_general_ci;

Let's break down each of components :
 `CREATE DATABASE dmoj` : create a new database named `dmoj`
`DEFAULT CHARACTER SET utf8mb4 ` : default character to store and encode for database is utf8mb4 (https://dev.mysql.com/doc/refman/8.0/en/charset-unicode-utf8mb4.html)
`DEFAULT COLLATE utf8mb4_general_ci` : collate means `collocation`. It sets default collocation for database to utf8mb4_general_ci https://dev.mysql.com/doc/refman/8.0/en/charset-unicode-sets.html

(*14)
mariadb> GRANT ALL PRIVILEGES ON dmoj.* TO 'dmoj'@'localhost' IDENTIFIED BY '<mariadb user password>';
Let's break down each of components :
`GRANT ALL PRIVILEGES` : it means that you give all privileges to Mariadb 
`ON dmoj.* ` : The asterisk (*) symbolises all the database tables that the user can access and perform addition, deletion, and modification operations on db table dmoj.
`TO 'dmoj'@'localhost' ` : 'dmoj' is the username, and 'localhost' is the host from which the user is allowed to connect => the user 'dmoj' is allowed to connect only from the localhost.
`IDENTIFIED BY '<mariadb user password>'` : This sets the password for the user 'dmoj'. Replace <mariadb user password> with the actual password you want to set for the 'dmoj' user.
(*15)
mariadb> exit


II) Create a virtual environment named melyojsite:


(*16)
` python3 -m venv melyojsite `

This command creates a virtual environment named melyojsite. It is an isolated Python environment that allows us to install, set up and manage dependencies separately for different projects.

For more detail : https://docs.python.org/3/library/venv.html#:~:text=The%20venv%20module%20supports%20creating,installed%20in%20their%20site%20directories.

(*17)
 `. melyojsite/bin/activate` : the command above, we created a virtual environment, so this command to activate it. The dot (.) at the beginning is a shortcut for the source command in Unix-like systems.


You'll avoid a lot of hassles during updates by keeping the necessary modules apart from the system package manager with the aid of the virtual environment.

Virtual environment : https://docs.python.org/3/tutorial/venv.html


Next, clone DMOJ's source code from the GitHub repository and prepare the environment for installation.

(*18) `git clone https://github.com/DMOJ/site.git` :
This command will copy the entire source code of DMOJ from the GitHub repository to our machine. The site folder will be created in your current directory.

(*19) `cd site` : cd stands for `change directory`, so we change directory to the folder `site` that we just created above

(*20) `git checkout v4.0.0` : check out a desired version
git checkout : switch branches (https://shorturl.at/akJMZ)
v4.0.0 : 

(*21) `git submodule init` : initialise submodule. Submodule allows us to add and manage repositories and keep them separate.
Submodule : https://git-scm.com/book/en/v2/Git-Tools-Submodules

(*22) `git submodule update`:  update submodule

After performing these steps, we have prepared our environment to continue installing dmoj

	+(*23)`pip3 install -r requirements.txt` : install the libraries and dependencies listed in the requirements.txt file into your Python environment.


+(*24)`pip3 install mysqlclient` : install mysql client. We found out mysqlclient above

Next, we are going to handle setting files ` dmoj/local_settings.py `
Take note : dmoj is not an app. It is a project




Why do we already have `settings.py ` and need to create `local_settings.py`?

=> Creating an additional local_settings.py file is often done to manage local settings and changes specific to each developer's development environment or specific settings, including security, easy restoration, version control

So, we gonna access to this link and make a copy of `local_settings.py`

https://github.com/DMOJ/docs/blob/master/sample_files/local_settings.py

Now, you check whether everything works or not ? 

If not, it probably returns the error

```python
System check identified some issues:

ERRORS:
?: (models.E001) Django 3.1 requires Python 3.6 or later.
```

So, it is the meaning of (*25)`python3 manage.py check`


III) Compiling assets:

There are two important concepts : SCSS & Autoprefixer CSS

SCSS : https://sass-lang.com/
Autoprefixer CSS : https://autoprefixer.github.io/

(*26)`./make_style.sh`
 
`./`  : it's url directory 
`make_style.sh` : The DMOJ uses sass and autoprefixer to generate the site stylesheets. The DMOJ comes with a `make_style.sh` script that may be run to compile and optimize the stylesheets.


(*27) `python3 manage.py collectstatic`
=> Each of the time, you make changes to css,scss or js. Run this command to collect assets again




(*28) `python3 manage.py compilemessages`

=> 

(*28) `python3 manage.py compilejsi18n`
=> apply multi-languages on the program

IV) Setting up database tables:

There is a need to create the structure or layout of the database tables, relationships, and constraints.

There are no tables or the existing tables do not have any structure defined yet. We set up to define the tables, specify the columns in each table, their data types, and any relationships between the tables. This process sets up the foundation for storing data in an organized and structured way.

For Django, we need to create and apply these changes to the database by these two familiar commands : `migrate` and `makemigrations`

Here, we just create tables into database, using :

(*29)`python3 manage.py migrate`

(*30) `python3 manage.py loaddata navbar` 
=> It loads data from a fixture file called `navbar`. In this case, it might be populating data related to navigation bars.

The `loaddata` command is a part of Django's serialization framework that allows you to import/export data to/from your database using fixture files.a

Find out fixture file here : https://docs.djangoproject.com/en/5.0/topics/db/fixtures/#:~:text=A%20fixture%20is%20a%20collection,multiple%20directories%2C%20in%20multiple%20applications. 


(*31)`python3 manage.py loaddata language_small`

=> Similar to the first command, this loads data into the database from a fixture file named `language_small`. This could be related to language settings or configurations.

(*32)`python3 manage.py loaddata demo`

Same as the previous command with a fixture file named `demo`. 

(*33)`python3 manage.py createsuperuser`

=> Create an admin account 


V) Setting up Celery:

Celery - distributed task queue system in Python





There are some stages to perform :

Install and run a Redis server. 
Configure Celery to use Redis as its message broker.
Deploy Celery workers that will perform various tasks related to the DMOJ system.

(*34)`service redis-server start`  : Ubunutu
(*34)`brew services start redis ` : macOs
=> Its function like its name `start Redis server`

Configure `local_settings.py` by uncommenting `CELERY_BROKER_URL` and `CELERY_RESULT_BACKEND`


VI) Running the server:


(*35)`python3 manage.py runserver` : run your django project 













Chapter 2 : Install DMOJ using docker (site and judge)



A judge includes `site-side` and `judge-side`

Seconds ….. !

What's the judge ?

Look at the photo below 




There is an algorithmic problem, and I execute my code for a solution. It returns `Error`, so it means that `the judge` will go through all test cases and check whether it correct or not


I will run commands on macOs. In case, you use a window operating system. You need to set up VNWare or Virtual Box, installing Ubuntu 22.04

[https://github.com/VietThienTran/DeploymentTools/tree/main/BQNOJ](https://github.com/VietThienTran/DeploymentTools/tree/main/BQNOJ)

Refer to the link above if your computer is using Ubuntu.

Step 1 : Install Docker and Docker compose

Follow its instruction on the web, https://docs.docker.com/compose/install/


Step 2 : Running the bridge :

Start your server 

`python3 manage.py runserver 0.0.0.0:8000`

Run the bridge :

`python3 manage.py runbridged`


Opening the file `local_settings.py` and find the `BRIDGED_JUDGE_ADDRESS`



You change `localhost` to your actual IP in your computer like your IP wifi

`BRIDGED_JUDGE_ADDRESS = [('localhost', 9999)]`

=> change your `localhost`


Step 3 : Add “JUDGE_AUTHENTICATION_KEY” and “JUDGE_NAME”:

You access to `/admin/`



and then, you create admin account to login 






Run this command `python3 manage.py createsuperuser`




Next, we click to `langues` and choose `add judge` to fill in the `judge name` and `authentication key`




Step 4 : Clone `judge server` and run 

`git clone --recursive https://github.com/DMOJ/judge.git`

it means that you clone `judge server` into your project




