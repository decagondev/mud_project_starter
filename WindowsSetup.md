As of 11/20/19 this should work with Python 3.6.8.  We will be using this version, unlike Mac users, who will use 3.8.  

1. [Make sure you have installed WSL, Ubuntu, Python, and Pipenv.](https://github.com/LambdaSchool/CS-Wiki/wiki/Installing-Python-3-and-pipenv#wsl)
2. Open cmd.exe as an administrator and start bash with `bash`
3. Using Gitbash, or whichever method you have been using, clone the repository for Build Week 2
4. Try `pipenv shell`.  If this fails, make sure that every reference in the error refers to Python 3.6.  If not, review the troubleshooting steps in the link above.
    1. If the error does refer to 3.6:
        1. Confirm that `python --version` refers to 2.7.something
        2. Confirm that `/usr/bin/python3 --version` refers to 3.6.8
        3. `pipenv --three --python=`which python3``  *NOTE* that there are backticks (`) around *which python3*
        4. This should create the shell forcing it to use 3.6.8
5. Open the `pipfile` and change the required version of Python to "3"
        1. *Your whole team will need to make this change*
        2. This should allow you to work with colleagues on Macs that have a higher version, but this has yet to be extensively tested. Please report your experiences to your instructors
6. [Install Postgres](https://github.com/michaeltreat/Windows-Subsystem-For-Linux-Setup-Guide/blob/master/readmes/installs/PostgreSQL.md)
    1. *Contrary to the instructions in step 1, do this process using the bash terminal opened in cmd.exe running as an administrator*
    2. Step 5 is a little confusing.  Paste it into the terminal and it will say `OK` and the `sudo apt-get update` will be entered as an unexecuted command.  Hit `Enter`
    3. If on Step 6 you get an error complaining about the version of libicu52 or similar install it with:
        1. sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main" 
        2. sudo apt-get update
        3. sudo apt-get install libicu55
        4. Complete User Setup from the same set of instructions
7. Install Postgres Server Side Extension:
    1. `sudo apt-get install libpq-dev`
8. Try `pipenv install`.  This may fail with an error about "psycopg2" related to being unable to find "pg_config"
    1. Fix with `export PATH=/usr/bin:$PATH` inside the shell
9. Try `pipenv install` again.  If you still have errors, please review the above or ask for help in the help channel
10. Enter the shell with `pipenv shell` and try `python manage.py showmigrations`.
    1. If this errors because Django is not found, install it: `pipenv install django`
    2. If this errors because "SECRET_KEY", "DEBUG", or other values are not found, set up a .env as described in the docs
    3. If you see a list of unapplied migrations, you should be ready to apply the migrations and get started
        1. If you try to run the server and get additional errors, make sure that you don't have unmade migrations:
            1. `python manage.py makemigrations` then `python manage.py migrate`
