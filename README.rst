Sample nginx + uWSGI stack for OpenShift
========================================

This is a collection of scripts that allows you to deploy a project running on
a nginx+uWSGI stack on OpenShift. 

Quick start
===========

In order to use this repository, you'll have to clone it and use it as the
main git repository on a `DIY OpenShift Cartridge`_.

First, create your app with ``rhc``:::
    
    $ rhc app create myapp diy-0.1

Now, add this repository to the created git repo and pull from it:::

    $ cd myapp
    $ git remote add upstream https://github.com/fcoelho/nginxdjango-openshift
    $ git pull -s recursive -X theirs upstream master

As a last step before pushing your changes, you'll need to create the
application that will be served by the stack. A ``app/wsgi.py`` script is
expected. Create it like the following:::

    $ mkdir app
    $ cat > app/wsgi.py << EOF
    def application(env, start_response):
        start_response('200 OK', [('Content-Type', 'text/html')])
        return ['Hello world']
    EOF

    $ git add app
    $ git commit -a -m 'sample application'

Now we're ready to push the changes to our OpenShift repository. Go get a
coffee, the scripts will build nginx, Python, and uWSGI from source, it might
take a while.::

    $ git push origin master

During the installation process, there will be some messages indicating
progress. A small spinner is used to show that connectivity hasn't been lost.

After the installation is done, you can access your application at
``myapp-<domain>.rhcloud.com``:::

    $ curl myapp-<domain>.rhcloud.com
    Hello world

Video
*****

There is a video of this process on `ASCII.IO <http://ascii.io/a/3286>`_. Note
that, although it is a simple process, building the software on the host
machines takes some time. The total running time of the above video is ~25min.
Feel free to skip through the ``make ...`` parts until I don't upload a better
video.

.. _DIY OpenShift Cartridge: https://www.openshift.com/developers/do-it-yourself
