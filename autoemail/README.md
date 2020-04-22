Denise Soriano  
Alexis Czezar Torreno  
Mel-Jie Bentz Del Mundo

***

# List of Directories and Important Notes About the Data

## Hierarchy

- Main directory: `submission_yyyy-mm-dd_hh-mm-ss_<num_of_iterations>`
	- Subdirectories (per dataset): `<dataset>_<num_of_iterations>`, e.g. `lang_5`
		- Iteration directories: `iteration#`, e.g. `iteration3`
			- `assoc_mem_<dataset>.csv`
			- `encoded_vectors_<dataset>.csv`
				- Format: `<dataset>,<label>,<vector>`
			- `item_memory.dat`
			- `logs`

## Notes

1. To minimize the run time, we changed `IEEG_PATS` to **6, 11, and 16** instead of choosing all 16 patients. *(Total run time = 00:01:27 for the three patients)*
2. **No randomization** was used in the encoded vectors; therefore there is no need to add test number in the encoded vectors because it is exactly in the order of test files.
3. Finally, we ran this code in Tensorflow version **2.0** instead of 2.1.
4. Datasets considered are **mer, emg, ieeg, feat, and lang**.

## Changes to the Original Code

1. Saved `assoc_mem_<dataset>` as **.csv** and not .npy.
2. In each **encode()** (per dataset.py), we used `tf.print()` to save the encoded test vectors into CSV. The vectors vary for each dataset hence it is different for each **encode()**.

## Additional Scripts

Since we have to iterate multiple times, the solution we did is we created a new Python script that runs the `make` commands `NUM_RUN` times. This is the **autoemail.py** script. To run:

	python autoemail.py <NUM_RUN>

Optional arguments:

- `--make` or `-m` specifies which datasets you want to iterate. Choose from `mer`, `emg`, `ieeg`, `feat`, `lang`, or `all`. Note that `python autoemail.py <NUM_RUN> --make all` is the same as `python autoemail.py <NUM_RUN>`.
- `--email` or `-e` if you want to email a copy of the zip file to the recipient/s of your choice. Specify the email recipients at *config.py*.

***

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
