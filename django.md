# Setup Development Environment

The preferred method to ensure consistency of development environments is to use Vagrant. Please see the [relevant document](docs/vagrant.md) to see how to set up Vagrant.

If you would like to set up this application directly on your machine (without a VM), please continue following the steps below.

1. Install [Python 3](https://www.python.org/downloads/)
2. Install Python 3 [Virtual Environment](https://docs.python.org/3/library/venv.html) (should be installed with Python3)
3. Clone the repository
4. In the root of the repo, create the virtualenv `pyvenv expo_venv`
5. Activate the virtual environment `source expo_venv/bin/activate`
6. Set up the Postgres DB as given below.
7. Set the debug environment variable to allow the site to know you are developing `export DJANGO_DEBUG=True`
8. Install the project requirements `pip install -r requirements.txt`
9. Move to the **gt_expo/** folder.
10. Run the Django test server and view the site: `python manage.py runserver`    

# Setup Postgres Database

Install Postgres:
- Mac, use homebrew and run `brew install postgres`.
- Linux, use your package manager. Some common setup instructions can be found [here](https://help.ubuntu.com/community/PostgreSQL). 

To create a database use the following commands:

    $ createdb `whoami` # creates a database and role for you
    $ psql     # you may have to pass in `-U postgres`
    >CREATE DATABASE expo_db;
    >CREATE USER expo WITH PASSWORD 'expo'; -- This should be the same as in the settings.py
    >GRANT ALL PRIVILEGES ON DATABASE expo_db TO expo;
    >\q

If you get the error `Role <username> does not exist`, then login to the postgres account `sudo -i -u postgres` and run

    $ createuser --interactive  # follow the commands to create a user with your account name
    $ createdb <username>

To access the database, use the following command: 
    
    >psql -U expo -d expo_db

The database needs to be populated with the tables. 
All the necessary migrations should be present in their respective app migration folders. Make sure to commit your updated migrations and avoid conflicts!
    
    python manage.py migrate
    
To get the dev database ready for operation, we need to add the fixture data. We have a script that does that for you. This script will also load in the test data needed.
Feel free to examine the script if you so wish to.

    cd test_data
    sh load_data.sh
     
To create updated fixtures, use the `dump_fixtures.sh` script
    
    cd test_data
    sh dump_fixtures.sh
    
## Database Operations

If you wish to clear a table, you can run the following command:

    python manage.py migrate <app_label> zero
    python manage.py migrate <app_label>
    
This will reset the tables in that app so you can use it for testing.

E.g. you may want to reset the judge app tables in order to try something new. In that case, just substitute `app_label` with `judge`.