# How to setup PyCharm for Talon



## Apply for professional account
In order to register for a professional account use please go to: https://www.jetbrains.com/student/


Apply:
![alt text](images/apply_student_account.png)


## Download PyCharm Professional
Go to: https://www.jetbrains.com/pycharm/ 

<br/>

Press Download:
![alt text](images/website_download.png)


<br/>

Choose Professional version [in this example I have use Linux. For Windows or Mac will be slightly different]:
![alt text](images/choose%20professional.png)


<br/>

## Install PyCharm:
Follow normal installation instruction

<br/>

**Fisrt time setup:**

<br/>

Skip Remaining and Set Defaults
![alt text](images/skip_remaining_set_default.png)


<br/>

Welcome to PyCharm
![alt text](images/welcome_pycharm.png)


<br/>

Go to Settings
![alt text](images/welcome_settings.png)


<br/>

Now click on Project Interpreter
![alt text](images/setting_interpretter.png)


<br/>

Click on right wheel
![alt text](images/settings_interpretter_add.png)



<br/>

Add...
![alt text](images/add_interpretter.png)


<br/>

SSH Interpreter
![alt text](images/ssh_interpretter.png)



<br/>

New server configuration: enter Talon Vis node address: vis-01.acs.unt.edu
![alt text](images/ssh_interpretter_username.png)



<br/>

Asks for Connecting To Remote Host: Accept **[It might ask for your password instead]**
![alt text](images/connection_remote_confirm_yes.png)


<br/>

It mgiht also ask you to enter password of your JetBrain account.
You created this account earlier. 
[Make sure to enter password for that account]
![alt text](images/login_unt_for_professional_verison.png)


<br/>

Default remote interpreter:
![alt text](images/current_interpretter.png)


<br/>

Brows to add a new interpreter:
![alt text](images/browse_interpretter.png)


<br/>

Enter path of Talon Python interpreter:
![alt text](images/enter_path_interpretter.png)


<br/>

Set path interpreter:
![alt text](images/set_path_interpretter.png)


<br/>

Path Interpreter should look like this now:
![alt text](images/finish_adding_interpretter.png)


<br/>

Project Interpreter should look like this now:
![alt text](images/inter-pretter_set.png)


<br/>

Need to wait for a while to finish:
![alt text](images/wait_to_finish_setup.png)


<br/>

## Test with creating a new project

<br/>

Create New Project
![alt text](images/test_create_new_project.png)


<br/>

Select Pure Python
Choose preffered name of project. In this case is **test**
Now we need to set interpreter:
![alt text](images/test_new_test_file.png)


<br/>

Click Project Interpreter > Existing Interpreter:
In **Remote project location** make sure add the path on Talon where you want your project to be!
![alt text](images/test_path_to_remote_server.png)


<br/>

Wait for some time:
![alt text](images/test_wait_before_workspace.png)


<br/>

If no folder is created wiht project name in Talon, PyCharm will create it for you.

<br/>

Create Python file:
![alt text](images/test_create_python_file.png)


<br/>

Name your python test file:
![alt text](images/test_create_file.png)


<br/>

File uploaded to Talon when it's created:
![alt text](images/test_file_uploaded.png)


<br/>

Write a print("Hello world!") in python file.
When save the file it will automatichally save it to Talon:
![alt text](images/test_hit_save_automatic_upload.png)


<br/>

To run the Python file:
![alt text](images/test_run_python_file.png)


<br/>

Python file will run on Talon and show results just like it's locally:
![alt text](images/test_python_file_is_running.png)


<br/>

To see files on Talon in PyCharm click **Remote Host** on right side:
![alt text](images/test_sroll_through_your_path.png)

<br/>
