Denise Soriano  
Alexis Czezar Torreno  
Mel-Jie Bentz Del Mundo

***

# List of Directories and Notes About the Data

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

Since we have to iterate multiple times, the solution we did is we created a new Python script that runs the `make` commands `NUM_RUN` times. This is the **wrapper.py** script. It also renames all the folders per iteration and per dataset.

The wrapper is then called by another script called **autoemail.py** which zips the submission folder and can automatically send the email to notify that you are done.

To run:

	python autoemail.py <NUM_RUN>

#### Optional arguments:

- `--make` or `-m` specifies which datasets you want to iterate. Choose from `mer`, `emg`, `ieeg`, `feat`, `lang`, or `all`. For more than one dataset, separate them with commas. Note that `python autoemail.py <NUM_RUN> --make all` is the same as `python autoemail.py <NUM_RUN>`.
- `--email` or `-e` if you want to email a copy of the zip file to the recipient/s of your choice. Specify the email recipients at *config.py*.

For example, if I want to run 6 iterations of just `mer`, `feat`, and `ieeg`, then email specific people to tell them when it's done:

	python autoemail.py 6 --make mer,feat,ieeg --email

This code can be edited to add more datasets in the accepted `make` commands list, such as `dna`. Just edit the `datasets` list in **autoemail.py**!

### Setting up Gmail account

If you want to use the email feature, a Gmail account is necessary. I couldn't get it to work with bmail though so you should use a different account with this. Set it up through these steps:

1. Enable POP and IMAP on your email (this can be found in Gmail settings).
2. Turn on 'less secure apps access' through this [link](https://myaccount.google.com/lesssecureapps?pli=1).

NOTE: This wouldn't work if you have 2-step verification on for your Gmail. To use this program, turn 2-step verification OFF.

### Configure Email Details

Input your email address and password inside **config.py**. **Don't show your password to anyone!**

Also input your hawk username and the recipient/s (as a list) in config.py.

NOTE: This programs assumes that you are working in the **hawk** server. If you are not working in this server, just change the `basepath` variable in the main of autoemail.py.
