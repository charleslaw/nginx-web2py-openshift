Sample nginx + uWSGI stack for OpenShift
========================================

This is a collection of scripts that allows you to deploy a project running
from a WSGI server. For the frontend, requests are parsed by nginx, and the
applications receives its requests from the uWSGI program.

Quick start
===========

In order to use this repository, you'll have to clone it and use it as the
main git repository on a `DIY OpenShift Cartridge`_


.. _DIY OpenShift Cartridge: https://www.openshift.com/developers/do-it-yourself
