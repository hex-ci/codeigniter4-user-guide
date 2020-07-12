############################
在命令行中运行
############################

除了通过在浏览器中输入 URL 的方式访问 :doc:`控制器 </incoming/controllers>` 外，我们还可以通过命令行界面（CLI）的方式调用程序。

.. contents::
    :local:
    :depth: 2

什么是 CLI ？
================

命令行界面是一个基于文本的与计算机交互的方式。更多内容请访问 `维基百科 <https://en.wikipedia.org/wiki/Command-line_interface>`_ 。

为什么要通过命令行的方式运行？
=============================

对于 CodeIgniter 而言，有很多理由需要你使用命令行。但他们并非显而易见。

-  无需使用 *wget* 或 *curl* 即可运行的定时脚本。
-  通过获取 :php:func:`is_cli()` 的返回值，使你的定时脚本无法通过 URL 访问。
-  编写交互式的“任务”，比如一些需要设置权限，修改缓存文件夹，执行备份等操作。
-  和其他语言编写的其他应用程序交互，比如：一个 C++ 脚本可以通过调用一个命令的方式在你编写的模块中执行。

让我们尝试一下: Hello World!
=============================

首先我们来新建一个简单的控制器，这样你就可以看到他的行为。使用你的编辑器，新建一个名为 Tools.php 的文件，并在文件中写入如下代码::

	<?php namespace App\Controllers;

        use CodeIgniter\Controller;

	class Tools extends Controller {

		public function message($to = 'World')
		{
			echo "Hello {$to}!".PHP_EOL;
		}
	}

然后将这个文件保存在 **app/Controllers/** 目录下。

通常你会使用如下的 URL 访问你的网站::

	example.com/index.php/tools/message/to

然而，我们现在要打开 Mac/Linux 下的 Terminal 或者在 Windows 下点击“运行”并输入“cmd”之后进入我们 CodeIgniter 项目的 web 根目录，并执行以下命令：

.. code-block:: bash

	$ cd /path/to/project/public
	$ php index.php tools message

如果你的操作正确，你将会看到这个输出 *Hello World!*

.. code-block:: bash

	$ php index.php tools message "John Smith"

我们可以在这里像传入 URL 参数一样，传入一个参数。“John Smith”这个参数作为输入得到的的输出如下::

	Hello John Smith!

这里是基础!
==================

简而言之，就是我们要知道命令行上的控制器。需要记住的是，这是一个真正的控制器，所以路由和 ``_remap()`` 都是正常运作的。

但是， CodeIgniter 提供了额外的工具，可以是更加轻松地创建 CLI 可访问的脚本：包括 CLI-only 路由和一个帮助你使用 CLI-only 工具的库。

CLI-Only 路由
----------------

在 **Routes.php** 文件中你可以像创建其他路由的方式轻松新建只能通过 CLI 方式访问的路由，这些路由并不是使用类似 ``get()`` 、
``post()`` ，或者其他类似的方法，在这里你需要使用 ``cli()`` 方法::

    $routes->cli('tools/message/(:segment)', 'Tools::message/$1');

更多信息，可以查看这里 :doc:`路由 </incoming/routing>` 。

CLI 类库
---------------

CLI 类库让我们的 CLI 工作变得简单。它提供了简单的方法让我们将多种颜色的文本输出在终端上。它还可以让你给用户输出提示信息，构建出一个更加智能的工具。

更多信息，可以查看这里 :doc:`CLI 类库 </cli/cli_library>` 。
