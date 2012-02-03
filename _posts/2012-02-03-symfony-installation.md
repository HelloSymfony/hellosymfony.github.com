---
layout: post
title: "Symfony ��װ"
category: 
tags: []
---
{% include JB/setup %}

.. index::
   single: Installation

��װ������Symfony
=================

���µ�Ŀ����������Ժܿ�ؿ�ʼ������һ�����õ�SymfonyӦ�á��������
Symfony�ṩ��һ������׼�����汾��������һ�����õ�Symfony���𲽡���Ŀ��
����������������׼�����汾�����̿�ʼ������

.. tip::
   
   �������Ѱ���������ѷ�ʽ��ʼһ������Ŀ������������汾���ƣ������
   `Using Source Controll`_��

����Symfony2�����汾
--------------------

.. tip::

   ���ȣ���ȷ�����Ѿ���װ�����ú���һ��web����������Apache����ͬʱ��װ��PHP
   5.3.2����߰汾�����˽����Symfony2��ϵͳҪ�󣬲��� :doc:`requirments reference</reference/requirments>`��

Symfony2�����һ���������汾��������һ�������������ܵ�Ӧ�ã���������Symfony2 ���ģ�core���⣬һЩ��ѡ��bundle��
һ�������Ŀ¼�ṹ������һЩĬ�ϵ����á���������һ��Symfony2�����汾��ͬʱ��Ҳ������һ�������������ܵ�Ӧ�ÿ�ܣ�
����Ի������Ӧ�ÿ�����̿�ʼ�������Լ���Ӧ�á�

���Ǵӷ���Symfony2����ҳ��`http://symfony.com/download`_��ʼ�������ҳ�棬��ῴ��һ��*Symfony ��׼��*������Symfony2
����Ҫ�ַ��汾����������Ҫ������ѡ��

* ������``.tgz``��������``.zip``��ʽ��ѹ���� - ��������һ���ģ������κ�һ��������������ĸ�ʽ��
* �Ƿ�����һ������vendors�ķ����汾�������ĵ������Ѿ���װ��`Git`_����
  Ӧ�����ز���vendors��Symfony2����Ϊ��������ʹ�õ��������ʱ��������һЩ���ԡ�

�����κ�һ��ѹ��������ѹ�����web��������Ŀ¼�¡���UNIX�����л����£����κ�һ�������������Խ�ѹ
����``###``�����������ļ�������

.. code-block:: bash
    
    # .tgz��ʽ
    tar zxvf Symfony_Standard_Vendors_2.0.###.tgz

    # .zip��ʽ
    unzip Symfony_Standard_Vendors_2.0.###.zip    

��ѹ����Ӧ����һ��``Symfony/``���ļ��У�Ŀ¼�ṹ���£� 

.. code-block:: text

    www/ <- ���web��Ŀ¼
        Symfony/ <- ��ѹ���ѹ����
            app/
                cache/
                config/
                logs/
            src/
                ...
            vendor/
                ...
            web/
                app.php
                ...

����Vendors
~~~~~~~~~~~

�������������˲�����vendors��ѹ��������������������������װvendors��

.. code-block:: bash
  
    php bin/vendors install

 ���������������б���ĵ�vendor�� - ����Symfony�Լ� - �� ``vendor/``Ŀ¼�¡�
 Ҫ�˽�Symfony2��ô����������⣬��ο�
 ":ref:`cookbook-managing-vendor-libraries`"��

���úͰ�װ
~~~~~~~~~~

��ĿǰΪֹ�����б���ĵ������ⶼ��``vendor/``Ŀ¼�¡�ͬʱ��``app/``Ŀ¼����һ��Ĭ�ϵ�Ӧ�����ã�
����һЩʾ��������``src/``Ŀ¼�¡�

Symfony2��һ�����ӻ������ò��Թ�����������ȷ�����web��������PHP��ȷ���ã��Ա�ʹ��Symfony���������URL��
���������ã�

.. code-block:: text
    
    http://localhost/Symfony/web/config.php

 �����鵽�����⣬���������Ǽ�����

 .. sidebar:: ����Ȩ��

      һ�������������web���������������û������``app/cache``��``app/logs``��дȨ�ޡ�
      ��UNIXϵͳ�ϣ�������web�������û����������û�����ͬһ���û���������������Ŀ��
      ����һ��һ�µ������ȷ����ȷ������Ȩ�ޡ���``www-data``��Ϊ���web�������û���

      **1. ��֧��chmod +a��ϵͳ����ACL**

      ���ϵͳ������������``chmod +a``�����������������д��󣬳�����һ���ķ�����

      .. code-block:: bash
          rm -rf app/cache/*
          rm -rf app/logs/*

        sudo chmod +a "www-data allow delete,write,append,file_inherit,directory_inherit" app/cache app/logs
        sudo chmod +a "`whoami` allow delete,write,append,file_inherit,directory_inherit" app/cache app/log

      **2. �ڲ�֧��chmod +a��ϵͳ����ACL**

      һЩϵͳ��֧��``chmod +a``����֧������һ�ֽ�``setfacl``�Ĺ��ߡ��������Ҫ�����Ӳ�̷�����`��ACL֧��`_��
      ��װsetfacl��Ȼ��������ʾ��ʹ�ã�

      .. code-block:: bash

          sudo setfacl -R -m u:www-data:rwx -m u:`whoami`:rwx app/cache app/logs
          sudo setfacl -dR -m u:www-data:rwx -m u:`whoami`:rwx app/cache app/logs

      **3. ����ACL**

      �����û��Ȩ�޸ı��ļ��е�ACL������Ҫ�޸�umash��ʹcache��log�ļ��кͶ�����
      �û����ȫ���û���д��ȡ����web���������������û��Ƿ���ͬһ���û��飩��Ҫ������һ�㣬
      �����зŵ�``app/console``��``web/app.php``��```web/app_dev.php``�Ŀ�ͷ��

      .. code-block:: php

          umash(0002); // �������Ȩ�ޱ�Ϊ0775

          // ��

          umash(0000); // �������Ȩ�ޱ�Ϊ0777

       ��Ҫע����ǣ��������Ȩ�޸����ļ���Ȩ�ޣ��Ƽ�ʹ��ACL����Ϊ�ı�umash����thread-safe�ġ�

��һ�ж�û����ʱ�����"Go to welcome page"��������ĵ�һ��������Symfony2��ҳ��

.. code-block:: text

    http://localhost/Symfony/web/app_dev.php/

��Ӧ�ûῴ��Symfony2��ӭ�����Ϣ��

.. image:: /images/quick_tour/welcome.jpg


��ʼ����
--------

����������һ��������ɹ��ܵ�Symfony2Ӧ�ã�����Կ�ʼ���������ˣ�������صķ����汾Ӧ�ð�������
ʾ������ - ����ͨ���鿴��ͬ�����汾��``README.rst``�ļ�����txt��ʽ�򿪣����˽�ʾ�����룬���˽�
����ں���������ɾ����Щ���롣

ʹ�ð汾����ϵͳ
----------------

�����ʹ��������``Git``��``Subversion``�İ汾����ϵͳ��������Լ����ã���ʼ�ύ��Ĵ��롣
Symfony��׼�����汾*��*������Ŀ����㡣

��Ҫ�˽��������õ�ʹ��git�����������Ŀ�� ����:doc:`/cookbook/workflow/new_project_git`��

����``vendor/``Ŀ¼
~~~~~~~~~~~~~~~~~~~

����������˲���vendors��ѹ����������Ժ�������``vendor/``�ļ��У������䱻�ύ���汾����ϵͳ��
������õ���``Git``�����Դ���һ��``.gitignore``���ļ�����������һ�У�

.. code-block:: text
    
    vendor/

���ڣ�vendor�ļ��в��ᱻ������ύ���汾���ơ������ܺã���ʵ�������ˣ�������Ϊ������clone��
check out�����Ŀʱ����/�����Լ򵥵�����``php bin/vendors install``�ű����������б����vendor
�⡣

.. _`enable ACL support`: https://help.ubuntu.com/community/FilePermissions#ACLs
.. _`http://symfony.com/download`: http://symfony.com/download
.. _`Git`: http://git-scm.com/
.. _`GitHub Bootcamp`: http://help.github.com/set-up-git-redirec


