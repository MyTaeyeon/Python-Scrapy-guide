.. _intro-install:

==================
Hướng dẫn cài đặt
==================

.. _faq-python-versions:

Các phiên bản python được hỗ trợ
=========================

Scrapy yêu cầu Python 3.8+, triển khai CPython (mặc định) hoặc triển khai PyPy.

.. _intro-install-scrapy:

Cài đặt Scrapy
=================

Nếu bạn đang sử dụng `Anaconda` hoặc `Miniconda`, bạn có thể cài đặt gói từ kênh `conda-forge`, kênh này có các gói cập nhật cho Linux, Windows và macOS.

Để cài đặt Scrapy bằng cách sử dụng ``conda``, hãy chạy:

  conda install -c conda-forge scrapy

Ngoài ra, nếu bạn đã quen với việc cài đặt các gói Python, bạn có thể cài đặt Scrapy và các phần phụ thuộc của nó từ PyPI bằng::

    pip install Scrapy

Chúng tôi thực sự khuyên bạn nên cài đặt Scrapy trong `virtualenv chuyên dụng` để tránh xung đột với các gói hệ thống của bạn.

Lưu ý rằng đôi khi điều này có thể yêu cầu giải quyết các vấn đề biên dịch đối với một số phụ thuộc Scrapy tùy thuộc vào hệ điều hành của bạn.

Để biết thêm hướng dẫn chi tiết và cụ thể về nền tảng cũng như thông tin khắc phục sự cố, hãy đọc tiếp.


Nên biết
----------------------------

Scrapy được viết bằng Python thuần túy và phụ thuộc vào một số gói Python chính (trong số các gói khác):

* `lxml`_, trình phân tích cú pháp XML và HTML hiệu quả
* `parsel`_, một thư viện trích xuất dữ liệu HTML/XML được viết trên lxml,
* `w3lib`_, một trình trợ giúp đa mục đích để xử lý các URL và mã hóa trang web
* `twisted`_, một khung mạng không đồng bộ
* `cryptography`_ và `pyOpenSSL`_, để giải quyết các nhu cầu bảo mật cấp mạng khác nhau

Bản thân một số gói này phụ thuộc vào các gói không phải Python và có thể yêu cầu các bước cài đặt bổ sung tùy thuộc vào nền tảng của bạn.

Sử dụng môi trường ảo (recommended)
-----------------------------------------

TL;DR: Chúng tôi khuyên bạn nên cài đặt Scrapy trong môi trường ảo trên tất cả các nền tảng.

Các gói Python có thể được cài đặt trên toàn hệ thống hoặc trong không gian người dùng. Chúng tôi khuyên bạn không nên cài đặt Scrapy toàn bộ hệ thống.

Thay vào đó, chúng tôi khuyên bạn nên cài đặt Scrapy trong cái gọi là “môi trường ảo” (`venv`).Môi trường ảo cho phép bạn không xung đột với các gói hệ thống Python đã được cài đặt sẵn (điều này có thể phá vỡ một số công cụ và tập lệnh hệ thống của bạn) và vẫn cài đặt các gói bình thường với `pip`(không có `sudo` và tương tự).

.. _intro-install-platform-notes:

Platform specific installation notes
====================================

.. _intro-install-windows:

Windows
-------

Though it's possible to install Scrapy on Windows using pip, we recommend you
to install `Anaconda`_ or `Miniconda`_ and use the package from the
`conda-forge`_ channel, which will avoid most installation issues.

Once you've installed `Anaconda`_ or `Miniconda`_, install Scrapy with::

  conda install -c conda-forge scrapy

To install Scrapy on Windows using ``pip``:

.. warning::
    This installation method requires “Microsoft Visual C++” for installing some 
    Scrapy dependencies, which demands significantly more disk space than Anaconda.

#. Download and execute `Microsoft C++ Build Tools`_ to install the Visual Studio Installer.

#. Run the Visual Studio Installer.

#. Under the Workloads section, select **C++ build tools**.

#. Check the installation details and make sure following packages are selected as optional components:

    * **MSVC**  (e.g MSVC v142 - VS 2019 C++ x64/x86 build tools (v14.23) )
    
    * **Windows SDK**  (e.g Windows 10 SDK (10.0.18362.0))

#. Install the Visual Studio Build Tools.

Now, you should be able to :ref:`install Scrapy <intro-install-scrapy>` using ``pip``.

.. _intro-install-ubuntu:

Ubuntu 14.04 trở lên
---------------------

Scrapy hiện đã được thử nghiệm với các phiên bản mới nhất của lxml, Twisted và pyOpenSSL, đồng thời tương thích với các bản phân phối Ubuntu gần đây. Nhưng nó cũng sẽ hỗ trợ các phiên bản Ubuntu cũ hơn, như Ubuntu 14.04, mặc dù có các vấn đề tiềm ẩn với kết nối TLS.

**Đừng** sử dụng ``python-scrapy`` gói do Ubuntu cung cấp, chúng thường quá cũ và chậm để bắt kịp Scrapy mới nhất.

.. _intro-install-macos:

macOS
-----

Building Scrapy's dependencies requires the presence of a C compiler and
development headers. On macOS this is typically provided by Apple’s Xcode
development tools. To install the Xcode command line tools open a terminal
window and run::

    xcode-select --install

There's a `known issue <https://github.com/pypa/pip/issues/2468>`_ that
prevents ``pip`` from updating system packages. This has to be addressed to
successfully install Scrapy and its dependencies. Here are some proposed
solutions:

* *(Recommended)* **Don't** use system Python. Install a new, updated version
  that doesn't conflict with the rest of your system. Here's how to do it using
  the `homebrew`_ package manager:

  * Install `homebrew`_ following the instructions in https://brew.sh/

  * Update your ``PATH`` variable to state that homebrew packages should be
    used before system packages (Change ``.bashrc`` to ``.zshrc`` accordingly
    if you're using `zsh`_ as default shell)::

      echo "export PATH=/usr/local/bin:/usr/local/sbin:$PATH" >> ~/.bashrc

  * Reload ``.bashrc`` to ensure the changes have taken place::

      source ~/.bashrc

  * Install python::

      brew install python

  * Latest versions of python have ``pip`` bundled with them so you won't need
    to install it separately. If this is not the case, upgrade python::

      brew update; brew upgrade python

*   *(Optional)* :ref:`Install Scrapy inside a Python virtual environment
    <intro-using-virtualenv>`.

  This method is a workaround for the above macOS issue, but it's an overall
  good practice for managing dependencies and can complement the first method.

After any of these workarounds you should be able to install Scrapy::

  pip install Scrapy


PyPy
----

We recommend using the latest PyPy version.
For PyPy3, only Linux installation was tested.

Most Scrapy dependencies now have binary wheels for CPython, but not for PyPy.
This means that these dependencies will be built during installation.
On macOS, you are likely to face an issue with building the Cryptography
dependency. The solution to this problem is described
`here <https://github.com/pyca/cryptography/issues/2692#issuecomment-272773481>`_,
that is to ``brew install openssl`` and then export the flags that this command
recommends (only needed when installing Scrapy). Installing on Linux has no special
issues besides installing build dependencies.
Installing Scrapy with PyPy on Windows is not tested.

You can check that Scrapy is installed correctly by running ``scrapy bench``.
If this command gives errors such as
``TypeError: ... got 2 unexpected keyword arguments``, this means
that setuptools was unable to pick up one PyPy-specific dependency.
To fix this issue, run ``pip install 'PyPyDispatcher>=2.1.0'``.


.. _intro-install-troubleshooting:

Troubleshooting
===============

AttributeError: 'module' object has no attribute 'OP_NO_TLSv1_1'
----------------------------------------------------------------

After you install or upgrade Scrapy, Twisted or pyOpenSSL, you may get an
exception with the following traceback::

    […]
      File "[…]/site-packages/twisted/protocols/tls.py", line 63, in <module>
        from twisted.internet._sslverify import _setAcceptableProtocols
      File "[…]/site-packages/twisted/internet/_sslverify.py", line 38, in <module>
        TLSVersion.TLSv1_1: SSL.OP_NO_TLSv1_1,
    AttributeError: 'module' object has no attribute 'OP_NO_TLSv1_1'

The reason you get this exception is that your system or virtual environment
has a version of pyOpenSSL that your version of Twisted does not support.

To install a version of pyOpenSSL that your version of Twisted supports,
reinstall Twisted with the :code:`tls` extra option::

    pip install twisted[tls]

For details, see `Issue #2473 <https://github.com/scrapy/scrapy/issues/2473>`_.

.. _Python: https://www.python.org/
.. _pip: https://pip.pypa.io/en/latest/installing/
.. _lxml: https://lxml.de/index.html
.. _parsel: https://pypi.org/project/parsel/
.. _w3lib: https://pypi.org/project/w3lib/
.. _twisted: https://twistedmatrix.com/trac/
.. _cryptography: https://cryptography.io/en/latest/
.. _pyOpenSSL: https://pypi.org/project/pyOpenSSL/
.. _setuptools: https://pypi.python.org/pypi/setuptools
.. _homebrew: https://brew.sh/
.. _zsh: https://www.zsh.org/
.. _Anaconda: https://docs.anaconda.com/anaconda/
.. _Miniconda: https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html
.. _Visual Studio: https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio
.. _Microsoft C++ Build Tools: https://visualstudio.microsoft.com/visual-cpp-build-tools/
.. _conda-forge: https://conda-forge.org/