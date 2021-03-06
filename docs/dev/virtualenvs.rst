Pipenv & 虚拟环境
====================

本教程将引导你完成安装和使用 Python 包。

它将向你展示如何安装和使用必要的工具，并就最佳做法做出强烈推荐。请记住，
Python 用于许多不同的目的。准确地说，你希望如何管理依赖项可能会根据
你如何决定发布软件而发生变化。这里提供的指导最直接适用于网络服务
（包括 Web 应用程序）的开发和部署，但也非常适合管理任意项目的开发和测试环境。

.. note:: 本指南是针对 Python 3 编写。但如果你由于某种原因仍然使用 Python 2.7，
  这些指引应该能够正常工作。

确保你已经有了 Python 和 pip
---------------------------------

在您进一步之前，请确保您有 Python，并且可从您的命令行中获得。
你可以通过简单地运行以下命令来检查：

.. code-block:: bash

    $ python --version

你应该得到像 ``3.6.2`` 之类的一些输出。如果没有 Python，请从 `python.org`_ 
安装最新的 3.x 版本，或参考本指南的 `安装 Python`_ 一节。

.. Note:: 如果你是新手，你会得到如下错误：
    
    .. code-block:: python

        >>> python
        Traceback (most recent call last):
          File "<stdin>", line 1, in <module>
        NameError: name 'python' is not defined

    这是因为此命令要在 *shell*（也称为 *终端* 或 *控制台*）中运行。有关使用操作系统的
    shell 并和 Python 进行交互的介绍，请参阅面向 Python 新手的 `入门教程`_。

另外，你需要确保 :ref:`pip` 是可用的。你可以通过运行以下命令来检查：

.. code-block:: bash

    $ pip --version

如果你使用 `python.org`_ 或 `Homebrew`_ 的安装程序来安装 Python，你应该已经有 pip 了。
如果您使用的是Linux，并使用操作系统的包管理器进行安装，则可能需要单独
`安装 pip <https://pip.pypa.io/en/stable/installing/>`_。

.. _入门教程: https://opentechschool.github.io/python-beginners/en/getting_started.html#what-is-python-exactly
.. _python.org: https://python.org
.. _Homebrew: https://brew.sh
.. _安装 Python: http://docs.python-guide.org/en/latest/starting/installation/


安装 Pipenv
-----------------

:ref:`Pipenv` 是 Python 项目的依赖管理器。如果您熟悉 Node.js 的 `npm`_ 或
Ruby 的 `bundler`_，那么它们在思路上与这些工具类似。尽管 :ref:`pip` 可以安装 Python 包，
但仍推荐使用 Pipenv，因为它是一种更高级的工具，可简化依赖关系管理的常见使用情况。

使用 ``pip`` 来安装 Pipenv：

.. code-block:: python

    $ pip install --user pipenv


.. Note:: 这进行了 `用户安装`_，以防止破坏任何系统范围的包。如果安装后, shell 中没有
     ``pipenv``，则需要将 `用户基础目录`_的 ``bin`` 目录添加到 ``PATH`` 中。您可以通过运行
    ``python -m site`` 找到用户库，它将打印包括用户基础的站点信息。例如，在 Linux 上，
    这将返回 ``USER_BASE: '~/.local'``，所以你需要在 ``PATH`` 中添加 ``~/.local/bin``。
    在 Linux 和 MacOS 上，您可以通过 `修改 ~/.profile`_ 永久地设置 ``PATH``。
    在 Windows 上，您可以在 `控制面板`_ 中永久设置用户的 ``PATH``。

.. _npm: https://www.npmjs.com/
.. _bundler: http://bundler.io/
.. _用户基础目录: https://docs.python.org/3/library/site.html#site.USER_BASE
.. _用户安装: https://pip.pypa.io/en/stable/user_guide/#user-installs
.. _修改 ~/.profile: https://stackoverflow.com/a/14638025
.. _控制面板: https://msdn.microsoft.com/en-us/library/windows/desktop/bb776899(v=vs.85).aspx

为你的项目安装包
------------------------------------

Pipenv 管理每个项目的依赖关系。要安装软件包时，请更改到您的项目目录（或只是本教程中的
一个空目录）并运行：

.. code-block:: bash

    $ cd myproject
    $ pipenv install requests

Pipenv 将在您的项目目录中安装超赞的 `Requests`_ 库并为您创建一个 ``Pipfile``。
:ref:`Pipfile` 用于跟踪您的项目中需要重新安装的依赖，例如在与他人共享项目时。
你应该得到类似的输出（尽管显示的确切路径会有所不同）：

.. code-block:: text

    Creating a Pipfile for this project...
    Creating a virtualenv for this project...
    Using base prefix '/usr/local/Cellar/python3/3.6.2/Frameworks/Python.framework/Versions/3.6'
    New python executable in ~/.local/share/virtualenvs/tmp-agwWamBd/bin/python3.6
    Also creating executable in ~/.local/share/virtualenvs/tmp-agwWamBd/bin/python
    Installing setuptools, pip, wheel...done.

    Virtualenv location: ~/.local/share/virtualenvs/tmp-agwWamBd
    Installing requests...
    Collecting requests
      Using cached requests-2.18.4-py2.py3-none-any.whl
    Collecting idna<2.7,>=2.5 (from requests)
      Using cached idna-2.6-py2.py3-none-any.whl
    Collecting urllib3<1.23,>=1.21.1 (from requests)
      Using cached urllib3-1.22-py2.py3-none-any.whl
    Collecting chardet<3.1.0,>=3.0.2 (from requests)
      Using cached chardet-3.0.4-py2.py3-none-any.whl
    Collecting certifi>=2017.4.17 (from requests)
      Using cached certifi-2017.7.27.1-py2.py3-none-any.whl
    Installing collected packages: idna, urllib3, chardet, certifi, requests
    Successfully installed certifi-2017.7.27.1 chardet-3.0.4 idna-2.6 requests-2.18.4 urllib3-1.22

    Adding requests to Pipfile's [packages]...
    P.S. You have excellent taste! ✨ 🍰 ✨

.. _Requests: https://python-requests.org


使用安装好的包
------------------------

现在安装了 Requests，您可以创建一个简单的 ``main.py`` 文件来使用它：

.. code-block:: python

    import requests

    response = requests.get('https://httpbin.org/ip')

    print('Your IP is {0}'.format(response.json()['origin']))

然后你就可以使用 ``pipenv run`` 运行这段脚本：

.. code-block:: bash

    $ pipenv run python main.py

你应该获取到类似的输出：

.. code-block:: text

    Your IP is 8.8.8.8

使用 ``$ pipenv run`` 可确保您的安装包可用于您的脚本。我们还可以生成一个新的 shell，
确保所有命令都可以使用 ``$ pipenv shell`` 访问已安装的包。


下一步
----------

恭喜，您现在知道如何安装和使用Python包了！ ✨ 🍰 ✨



更低层次: virtualenv
=======================

`virtualenv <http://pypi.python.org/pypi/virtualenv>`_ 是一个创建隔绝的Python环境的
工具。virtualenv创建一个包含所有必要的可执行文件的文件夹，用来使用Python工程所需的包。

它可以独立使用，代替Pipenv。

通过pip安装virtualenv：

.. code-block:: console

  $ pip install virtualenv

测试你的安装

.. code-block:: console

   $ virtualenv --version

基本使用
~~~~~~~~~~~

1. 为一个工程创建一个虚拟环境：

.. code-block:: console

   $ cd my_project_folder
   $ virtualenv my_project

``virtualenv my_project`` 将会在当前的目录中创建一个文件夹，包含了Python可执行文件，
以及 ``pip`` 库的一份拷贝，这样就能安装其他包了。虚拟环境的名字（此例中是 ``my_project`` ）
可以是任意的；若省略名字将会把文件均放在当前目录。

在任何你运行命令的目录中，这会创建Python的拷贝，并将之放在叫做 :file:`my_project` 
的文件中。

你可以选择使用一个Python解释器（比如``python2.7``）：

.. code-block:: console

   $ virtualenv -p /usr/bin/python2.7 my_project

或者使用``~/.bashrc``的一个环境变量将解释器改为全局性的：

.. code-block:: console

   $ export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python2.7


2. 要开始使用虚拟环境，其需要被激活：

.. code-block:: console

   $ source my_project/bin/activate

当前虚拟环境的名字会显示在提示符左侧（比如说 ``(my_project)你的电脑:你的工程 用户名$）
以让你知道它是激活的。从现在起，任何你使用pip安装的包将会放在 ``my_project`` 文件夹中，
与全局安装的Python隔绝开。

像平常一样安装包，比如：

.. code-block:: console

    $ pip install requests

3. 如果你在虚拟环境中暂时完成了工作，则可以停用它：

.. code-block:: console

   $ deactivate

这将会回到系统默认的Python解释器，包括已安装的库也会回到默认的。

要删除一个虚拟环境，只需删除它的文件夹。（要这么做请执行  ``rm -rf my_project`` ）

然后一段时间后，你可能会有很多个虚拟环境散落在系统各处，你将有可能忘记它们的名字或者位置。

其他注意
~~~~~~~~~~~

运行带 ``--no-site-packages`` 选项的 ``virtualenv`` 将不会包括全局安装的包。
这可用于保持包列表干净，以防以后需要访问它。（这在 ``virtualenv`` 1.7及之后是默认行为）

为了保持你的环境的一致性，“冷冻住（freeze）”环境包当前的状态是个好主意。要这么做，请运行：

.. code-block:: console

    $ pip freeze > requirements.txt

这将会创建一个 :file:`requirements.txt` 文件，其中包含了当前环境中所有包及
各自的版本的简单列表。你可以使用 “pip list”在不产生requirements文件的情况下，
查看已安装包的列表。这将会使另一个不同的开发者（或者是你，如果你需要重新创建这样的环境）
在以后安装相同版本的相同包变得容易。

.. code-block:: console

    $ pip install -r requirements.txt

这能帮助确保安装、部署和开发者之间的一致性。

最后，记住在源码版本控制中排除掉虚拟环境文件夹，可在ignore的列表中加上它。

.. _virtualenvwrapper-ref:

virtualenvwrapper
-----------------

`virtualenvwrapper <https://virtualenvwrapper.readthedocs.io/en/latest/index.html>`_ 
提供了一系列命令使得和虚拟环境工作变得愉快许多。它把你所有的虚拟环境都放在一个地方。

安装（确保 **virtualenv** 已经安装了）：

.. code-block:: console

  $ pip install virtualenvwrapper
  $ export WORKON_HOME=~/Envs
  $ source /usr/local/bin/virtualenvwrapper.sh

(`virtualenvwrapper 的完整安装指引 <https://virtualenvwrapper.readthedocs.io/en/latest/install.html>`_.)

对于Windows，你可以使用 `virtualenvwrapper-win <https://github.com/davidmarble/virtualenvwrapper-win/>`_ 。

安装（确保 **virtualenv** 已经安装了）：

.. code-block:: console

  $ pip install virtualenvwrapper-win

在Windows中，WORKON_HOME默认的路径是 %USERPROFILE%\Envs 。

基本使用
~~~~~~~~~~~

1. 创建一个虚拟环境：

.. code-block:: console

   $ mkvirtualenv my_project

这会在 :file:`~/Envs` 中创建 :file:`my_project` 文件夹。

2. 在虚拟环境上工作：

.. code-block:: console

   $ workon my_project

或者，你可以创建一个项目，它会创建虚拟环境，并在 ``$PROJECT_HOME`` 中创建一个项目目录。
当你使用 ``workon myproject`` 时，会 ``cd`` -ed 到项目目录中。

.. code-block:: console

   $ mkproject myproject

**virtualenvwrapper** 提供环境名字的tab补全功能。当你有很多环境，
并且很难记住它们的名字时，这就显得很有用。

``workon`` 也能停止你当前所在的环境，所以你可以在环境之间快速的切换。

3. 停止是一样的：

.. code-block:: console

   $ deactivate

4. 删除：

.. code-block:: console

   $ rmvirtualenv my_project

其他有用的命令
~~~~~~~~~~~~~~~~~~~~~

``lsvirtualenv``
  列举所有的环境。

``cdvirtualenv``
  导航到当前激活的虚拟环境的目录中，比如说这样你就能够浏览它的 :file:`site-packages` 。

``cdsitepackages``
  和上面的类似，但是是直接进入到 :file:`site-packages` 目录中。

``lssitepackages``
  显示 :file:`site-packages` 目录中的内容。

`virtualenvwrapper 命令的完全列表 <https://virtualenvwrapper.readthedocs.io/en/latest/command_ref.html>`_ 。

virtualenv-burrito
------------------

有了 `virtualenv-burrito <https://github.com/brainsik/virtualenv-burrito>`_ ，
你就能使用单行命令拥有virtualenv + virtualenvwrapper的环境。

autoenv
-------
当你 ``cd`` 进入一个包含 :file:`.env` 的目录中，就会 `autoenv <https://github.com/kennethreitz/autoenv>`_ 
自动激活那个环境。

使用 ``brew`` 在Mac OS X上安装它：

.. code-block:: console

   $ brew install autoenv

在Linux上:

.. code-block:: console

   $ git clone git://github.com/kennethreitz/autoenv.git ~/.autoenv
   $ echo 'source ~/.autoenv/activate.sh' >> ~/.bashrc
