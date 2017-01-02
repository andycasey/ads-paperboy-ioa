Installation
============

Clone this repository using this terminal command:

    git clone git@github.com:andycasey/ads-paperboy-ioa.git paperboy


Setting up your Python installation
-----------------------------------

This code was written for Python version 2.7 due to the dependency requirements.
You can set your preferred Python flavour as version 2.7 on the IoA computers by 
adding the following command to the `.profile` file in your home directory:

    module load python/2.7 

Some Python packages will be installed to your home directory, so in the same 
`.profile` file you should add this line after the `module load python/2.7` line:

    export PYTHONPATH=$PYTHONPATH:/home/hurnm/.local/lib/python2.7/site-packages

After these lines have been added, either open a new terminal or enter 
`source ~/.profile` in your current terminal window.


Installing required Python packages
-----------------------------------

The code requires a few custom Python packages which can be installed with the 
following terminal command:

    pip install ads PyPDF2 --user 


Getting an ADS key
------------------

The NASA Astrophysics Data System (ADS) has an Application Programmer Interface 
(API) which allows us to run programmatic queries against their database. This 
service puts load on the ADS servers, and therefore could be overloaded by
unscrupulous users making too many requests. Therefore you will need to get a 
unique API token from ADS. We will use that token for all of the requests we 
make to ADS.

Here is how to get an API key from ADS:

  1. Sign up for an account on the [newest version of ADS](https://ui.adsabs.harvard.edu).

  2. Log in to your new account and navigate to [API Token](https://ui.adsabs.harvard.edu/#user/settings/token),
     and then click *Generate a new key*.

  3. Create a folder called `.ads` (the dot is necessary) in your home 
     directory and create a new file in the `.ads` folder called `dev_key`. 
     Save your generated key to the `dev_key` file.


Run the script
--------------

Now you should be able to run the `paperboy_ioa.py` script using the following 
terminal command:

    python paperboy_ioa.py 

This should produce some output to the terminal, and send an email with the 
papers published from the previous month. You can also specify the year and
month to search. For example:

    python paperboy_ioa.py 2014 8

Will search for papers published by IoA researchers in the month of August, 2014.


Set up a monthly Cron job to run the script automatically
---------------------------------------------------------

At a terminal, type:

    crontab -e

And enter in the following line:

    0 7 1 * * /opt/ioa/software/python/2.7/bin/python <YOUR_FOLDER>/paperboy_ioa.py > <YOUR_FOLDER>/paperboy.log

Then the code will run at 07:00 AM on the first day of every month. The 
`<YOUR_FOLDER>` expression above refers to the folder location where this script
lives on your local system.
