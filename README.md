## Overview
This project presents a high-level overiew of Python and Jupyter Notebook and how you can use these tools to do some basic data analysis. 

## Data used in this project
Publicly available data used in this project:
 - https://docs.celonis.com/en/event-log-sample-files.html


## Setup
### Pre-Requisites
This project has two system pre-requisites:
 - Anaconda (https://www.anaconda.com/download/)
 - Visual Studio Code, often simply refered to as "VS Code" (https://code.visualstudio.com/download)

Within VS Code, you should install the Python and Jupyter extensions from Microsoft:
 - https://marketplace.visualstudio.com/items?itemName=ms-python.python
 - https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter

### Project Setup
I've only tested this project in Python 3.10, but it will likely work in most Python 3.6 and above environments.  To set up the project, do the following:

#### Step 1: Use "conda" to install a minimal Python 3.10 environment on your machine
Launch a command shell and run the following:
``` bash
PS > conda create --name py3_10 python=3.10
```

Note that your minimal Python 3.10 environment will be installed to the environment location defined in your ```.condarc``` file.  For more details, see these links:
 - https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html
 - https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

#### Step 2: Change directory to your project directory
If you haven't created a project directory, do that first:
``` bash
PS > cd C:\Users\<your_user>\projects\hs_training
```

#### Step 3: Use "venv" to create a virtual Python environment for your project to use
The venv utility helps you create an isolated Python environment for just your project.  That way, if your project has specific dependencies, you can install those dependencies in your project's isolated environment without worrying about interfering with other Python projects on your machine.  Since we want to create an isolated environment based on Python 3.10, we'll use the Python interpreter we installed earlier with _conda_ to create our virtual environment:
``` bash
PS > C:\Users\<your_user>\conda_envs\py3_10\python -m venv app-env
```

> __Side note: Naming your virtual environment__
> 
> In many tutorials on the venv utility, you'll see people name their virtual environment "venv" after the tool they're using to create it.  Personally, I find that confusing, so I tend to avoid that practice and name my environment something more distinctive, like "app-env".  Other times, you'll see people add a period prefix to their environment name, eg. ".venv".  This can be a helpful practice, particularly if you're deploying your solution to a Unix-based system as Unix-based systems usually hide directories that start with a period.

#### Step 4: Launch VS Code
Since you're already in your project directory, it's easy to open it in VS Code:
``` bash
PS > code .
```

The VS Code Python extension is pretty smart.  It _should_ see the new virtual environment you created in Step 3 and immediately bind your project to that interpreter.  You can verify that in the blue status bar at the bottom of the VS Code window.  Also, as soon as you open a terminal window in VS Code, it should "activate" your virtual environment--that is, make the tools of your virtual environment available for use in your terminal.  If your VS Code was not this smart, see here:
https://stackoverflow.com/questions/68995862/how-to-activate-virtual-env-in-vs-code

#### Step 5: Install the required Python packages
Proper data analysis often relies on specialized packages outside the core Python installation.  This project will demonstrate how we use many of these packages, but we must first install them into the virtual environment by running the following within an "activated" terminal:
``` bash
(app-env) PS > pip3 install -r requirements.txt
```

> __Side note: Does your organization actively manage developer dependencies in some way?__
> 
> A term you should get to know is [DevOps](https://en.wikipedia.org/wiki/DevOps).  It is a general term that impacts how software developers (and data analysts) write their solutions, deploy them, and monitor them thereafter.  Your organization's approach to DevOps could also include managing the open source and third party packages on which your solutions depend.
> 
> A popular way organizations manage developer dependencies is through on-network binary repository managers like [Artifactory](https://jfrog.com/blog/what-is-artifactory-jfrog).  If this sounds like your organization, you may have to take additional steps to "pip install" the dependencies for this project.  For example, you may need to setup an environment variable to let the pip utility know to make no attempt to authenticate to your network's [Proxy server](https://www.fortinet.com/resources/cyberglossary/proxy-server) when attempting to load dependencies from your management server.  In PowerShell, that would be a command like this:
> 
> ```(app-env) PS > $env:no_proxy="my_dependency_repo"```
> 
> And then, when you run your "pip install" command, you'd include additional arguments like so:
> 
> ```(app-env) PS > pip3 install -r requirements.txt --trusted-host my_dependency_repo --index-url "appropriate url to your repo"```

#### Step 6: Register your virtual environment as a "kernel" for your Jupyter Notebooks
In order to leverage our virtual environment in our project--predominantly Jupyter Notebooks--we need to first register our virtual environment as a viable Jupyter Notebook "kernel":
``` bash
(app-env) PS > ipython kernel install --user --name=app-env
```

#### Step 7: Configure your Jupyter Notebooks
This project already contains several Jupyter Notebooks.  You should ensure that the notebooks:
 - are running on your locally installed Jupyter Notebook server by opening a notebook and checking that "Jupyter Server: local" is listed in the right-hand side of the blue VS Code status bar and 
 - "app-env" is listed in the upper right-hand corner of the notebook as the notebook's selected "kernel"

> __The kernel failed to start as the Python Environment...__
> 
> If you run into this problem, [this Stack Overflow post](https://stackoverflow.com/questions/70506366/failed-to-start-the-kernel-jupyter-in-vs-code/72937056#72937056) is helpful.  I did the following (in an activated shell):
> 
> ```(app-env) PS > pip3 install --upgrade pyzmq```
> 
> ```(app-env) PS > pip3 install jupyter```

> __Want to learn more about virtual environments and packaging?__
> 
> Check out [this great episode](https://talkpython.fm/episodes/show/436/an-unbiased-evaluation-of-environment-and-packaging-tools) of the [Talk Python to Me podcast](https://talkpython.fm/).  Also see [this associated blog post](https://alpopkes.com/posts/python/packaging_tools/).
