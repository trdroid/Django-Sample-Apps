> $ sudo apt-get -y install python-pip


Create an isolated Python environment 

<b>Installing virtualenv</b>

virtualenv can be used to create isolated Python environments so that different versions of packages can be installed as required by different projects. This is a recommended approach when compared to installing the packages system-wide. 

> $ sudo pip install virtualenv

<b>Specifying virtualenv which python version to use</b>

If the system has multiple python versions, the version of python to be used can be specified when creating the virtual environment

<i>Create an isolated Python environment 'vir_env' with the default python version on the system</i>

> $ which python

    /usr/bin/python

> $ python --version

    Python 2.7.6

> $ virtualenv vir_env

This creates a directory vir_env in the current working directory and a Python environment.

<i>Create an isolated Python environment 'vir_env' with the another python version on the system</i>

> $ which python3

    /usr/bin/python3

> $ python3 --version

    Python 3.4.3

> $ vir_env -p /usr/bin/python3

    Running virtualenv with interpreter /usr/bin/python3
    Using base prefix '/usr'
    New python executable in /home/droid/scratchpad/Django/vir_env/bin/python3
    Also creating executable in /home/droid/scratchpad/Django/vir_env/bin/python
    Installing setuptools, pip, wheel...done.

> $ ls vir_env/

    bin  lib

<b>Activate virtual environment</b>

Activate the virutal environment which displays the name of the active virual envionment enclosed in parentheses in the shell prompt.

> $ source vir_env/bin/activate

    (vir_env) droid@droidserver:~/scratchpad/Django$

Python libraries installed when a virtual environment is active are saved under directory:

<i>\<virtual-environment-directory\>/lib/\<python-version\>/site-packages</i>

eg. vir_env/lib/python3.4/site-packages

