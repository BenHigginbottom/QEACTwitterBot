# QEACTwitterBot

To take some of the load off the UK Defence Journal who for the past few months have been fighting the noble fight against people on twitter saying silly things about HMS Queen Elizabeth, such as "its leaking", "got no jets" etc, I've written this bot to send some form responses.



## Pre-requisites

Tested with Python 2.7, so this could be run on a Raspberry Pi 

Only external dependency is Tweepy, which assuming pip is installed, can be installed with the following command (Linux)

```bash
pip install tweepy --user
```

All testing has been conducted on Ubuntu Linux, although there isnt anything that would prevent it running on OSX or even Windows

## Setup

There are multiple tutorials on how to setup an app in twitter, so I'll just link to one -

https://dototot.com/how-to-write-a-twitter-bot-with-python-and-tweepy/

The application will need to be able to read and write to Twitter

## Configuration

With the Consumer and Access keys, the following section of the TwitterBot.py file will need to be updated

```python
CONSUMER_KEY = "CONSUMER_KEY"
CONSUMER_SECRET = "CONSUMER_SECRET"
ACCESS_TOKEN = "ACCESS_TOKEN"
ACCESS_TOKEN_SECRET = "ACCESS_TOKEN_SECRET"
```

We can then setup the search query to find general comments about Aircraft Carriers and the Queen Elizabeth, like so

```python
query = "Queen Elizabeth OR Aircraft Carrier AND jet OR aircraft OR leak OR sink"
```

Because these are rather general terms, we then can setup a series of python dictionaries that contain specific phrases to filter the search on and then reply to the people who dont think highly complex pieces of machinery need extensive testing...

These filters are easily expandable (although not 100% guranteed)

```python
aircraft = [ "no aircraft",
            "without aircraft",
            "aircraftless",
            "planeless",
            "no planes",
            "without planes"]

jets = ["no jets",
        "jetless",
        "without jets"]

leaking = ["is sinking",
           "is leaking",
           "leaks",
           "leak"]

```

And we now have the default responses to send for each of the search terms 

```python
raircraft = "Helicopters are aircraft"
rjets = "The F35 testing begins later this year"
rleaks = "This is what sea trials are for, issues will be found and fixed!"
```

After this is the core logic, which "should not" need editing!

## Running

```bash
python ./TwitterBot_QEAC.py
```

The program maintains a state in a textfile in the same directory as the program. This file contains the last ID of the tweet quoted and will only update the status if there is a new tweet.

There isnt a timer or other daemon yet, so the program will either need to be manually run or setup with a crontab

## To-do

* Convert into a lambda function (with a cloudwatch event trigger)
* State in dynamodb?