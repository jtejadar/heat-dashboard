Use Heat Dashboard in DevStack
------------------------------

Set up your ``local.conf`` to enable heat-dashboard::

    [[local|localrc]]
    enable_plugin heat-dashboard https://git.openstack.org/openstack/heat-dashboard

Manual Installation
-------------------

Clone both Horizon and Heat Dashboard repositories::

    git clone https://github.com/openstack/horizon
    git clone https://github.com/openstack/heat-dashboard

Create a virtual environment and install Horizon relevant packages::

    pip install -r horizon/requirements.txt

Create your ``local_settings.py`` file::

    cp horizon/openstack_dashboard/local/local_settings.py.example \
      horizon/openstack_dashboard/local/local_settings.py

Open newly created ``local_settings.py`` with your text editor,
and set some parameter to connect to your OpenStack environment:

- Set ``OPENSTACK_HOST`` as hostname or IP address of your OpenStack server.

- Verify that the ``OPENSTACK_KEYSTONE_URL`` and
   ``OPENSTACK_KEYSTONE_DEFAULT_ROLE`` settings are correct for your
   environment. (They should be correct unless you modified your
   OpenStack server to change them.)


Enable heat-dashboard plugin in your Horizon environment::

    cp heat-dashboard/heat_dashboard/enabled/* \
      horizon/openstack_dashboard/local/enabled

Finally you can launch Horizon with Heat Dashboard plugin::

    cd horizon
    python manage.py runserver 0.0.0.0:8080

Now you can connect to your Horizon including Heat Dashboard plugin
from your browser with URL http://localhost:8080/.