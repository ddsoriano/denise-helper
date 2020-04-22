# Guide to Using autoemail.py

Hello and welcome to the autoemail.py usage guide! This program simply runs all the 5 `make` commands `NUM_RUN` times, stores all build directories (1 per class) and zips them into one giant directory. The zip file is then emailed to the person/s of your choice automatically.

No additional libraries are needed for this code.

### Setting up Gmail account

For this program, it is necessary for you to use a Gmail account to send the files. To do that, here are the following steps:

1. Enable POP and IMAP on your email (this can be found in Gmail settings).
2. Turn on 'less secure apps access' through this [link](https://myaccount.google.com/lesssecureapps?pli=1).

NOTE: This wouldn't work if you have 2-step verification on for your Gmail. To use this program, turn 2-step verification OFF.

### Setting up the files

NOTE: This programs assumes that you are working in the **hawk** server. If you are not working in this server, just change the `basepath` variable in the main of autoemail.py

1. Import **autoemail.py**, **config.py**, and **wrapper.py** to your *hdc_tensorflow_v3* folder. The latest working version should be stored in the *scratch* folder.
2. Open **config.py** and fill in all the fields. If you are having trouble, the comment beside each variable should explain what and how you should write. Anytime you want to change your email address, or add/remove recipients, just change it in the config file.

### Running the code

Base usage:

	python autoemail.py <NUM_RUN>

where `NUM_RUN` is the number of iterations. So if you want to run each class 10 times:

	python autoemail.py 10

To ensure that the program continues to run even when you are disconnected from the server, `nohup` is suggested to put before the `python` command.

This runs all classes. If you only want to run one or just a few of the classes, the syntax is:

	python autoemail.py <NUM_RUN> --make <class>

where `class` can be either of the following: **mer**, **emg**, **feat**, **lang**, or **ieeg**. **all** is also an option -- but that is redundant. To run more than one of these, just separate each class by a comma:

	python autoemail.py 10 --make mer,lang,emg

`-m` can also be used instead of `--make`.

### Checking

Once the program is done, you should have sent an email with a zip file that starts with the word *submission*. You can also check the contents of the submission folder that should be created in your directory.