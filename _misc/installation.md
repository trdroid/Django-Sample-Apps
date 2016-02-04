### Create an isolated Python environment 

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

<b>Deactivate virtual environment</b>

> $ deactivate

### Installing Django

Get pip (pre-installed with Python >= 3.5)

> $ sudo apt-get -y install python-pip

Install Django in the virtual environment

> $ (vir_env) droid@droidserver:~/scratchpad/Django$ pip install Django==1.9.2

    Collecting Django==1.9.2
      Downloading Django-1.9.2-py2.py3-none-any.whl (6.6MB)
        100% |████████████████████████████████| 6.6MB 29kB/s 
    Installing collected packages: Django
    Successfully installed Django-1.9.2

Django gets installed in <i>vir_env/lib/python3.4/site-packages</i>

> $ ls vir_env/lib/python3.4/site-packages

    django  Django-1.9.2.dist-info  easy_install.py  _markerlib  pip  pip-8.0.2.dist-info  pkg_resources  __pycache__  setuptools  setuptools-19.6.2.dist-info  wheel  wheel-0.26.0.dist-info

Verify if Django has been installed

> $ (vir_env) droid@droidserver:~/scratchpad/Django$ python3

    Python 3.4.3 (default, Oct 14 2015, 20:28:29) 
    [GCC 4.8.4] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import django
    >>> django.VERSION
    (1, 9, 2, 'final', 0)

