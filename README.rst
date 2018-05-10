
=====================
model-manager formula
=====================

Model-manager is a service for manipulating the metadata models of the
SaltStack/reclass based deployments. It covers model management at various
stages of deployment life-cycles.

.. image:: doc/source/_static/img/stargate.png
   :width: 60%
   :align: center

Use cases for the model-manager service are:

* Streamline the model generation of complex infrastructures
* Wath the deployment process installing services across infrastructure
* Align monitoring checks and metrics to infrastructure


Sample metadata
===============

model-manager service with Keystone authentication

.. code-block:: yaml

    model_manager:
      server:
        enabled: true
        secret_key: supersecretkey
        source:
          engine: git
          address: https://github.com/salt-formulas/django-model-manager.git
          revision: master
        identity:
          engine: keystone
          host: keystone.endpoint.com
          protocol: https
          api_version: 3

model-manager service with model generator and Jenkins integration and HTTP remote

.. code-block:: yaml

    model_manager:
      server:
        enabled: true
        config_files:
        - _4000_integration
        - _4010_models_panel_group
        - _4020_integration_overview_panel
        - _4030_integration_modeldesigner_panel
        integration:
          engine: jenkins
          protocol: http
          host: 127.0.0.1
          port: 8080
          user: model-manager
          password: password
          model_template:
            job: generator-job
            remote: http
            url: https://git.my-gitlab.io/group/project/raw/master/context.yaml

model-manager service with model generator and Jenkins integration and localfs remote

.. code-block:: yaml

    model_manager:
      server:
        enabled: true
        config_files:
        - _4000_integration
        - _4010_models_panel_group
        - _4020_integration_overview_panel
        - _4030_integration_modeldesigner_panel
        integration:
          engine: jenkins
          protocol: http
          host: 127.0.0.1
          port: 8080
          user: model-manager
          password: password
          model_template:
            job: generator-job
            remote: localfs
            path: /etc/model-manager/cookiecutter-context.yaml

model-manager service with Gerrit remote and dynamic versioning enabled

.. code-block:: yaml

    model_manager:
      server:
        enabled: true
        config_files:
        - _4000_integration
        - _4010_models_panel_group
        - _4020_integration_overview_panel
        - _4030_integration_modeldesigner_panel
        integration:
          engine: jenkins
          protocol: http
          host: 127.0.0.1
          port: 8080
          user: model-manager
          password: password
          model_template:
            job: generator-job
            remote: gerrit
            url: https://my-gerrit.com
            project_name: full%2Fproject-name
            file_name: cookiecutter_context.yaml
            username: foo
            password: bar
            versioning:
              enabled: true
              filter: <regex>
              map:
                foo: bar

model-manager service with Salt master integration

.. code-block:: yaml

    model_manager:
      server:
        enabled: true
        config_files:
        - _5000_delivery
        - _5010_resource_management_panel_group
        - _5020_delivery_resource_topology_panel
        - _5030_delivery_salt_control_panel
        delivery:
          engine: salt
          protocol: http
          host: 127.0.0.1
          port: 6969
          user: model-manager
          password: password


More information
================

* http://salt-formulas.readthedocs.io/en/latest/develop/overview-reclass.html


Documentation and bugs
======================

To learn how to install and update salt-formulas, consult the documentation
available online at:

    http://salt-formulas.readthedocs.io/

In the unfortunate event that bugs are discovered, they should be reported to
the appropriate issue tracker. Use GitHub issue tracker for specific salt
formula:

    https://github.com/salt-formulas/salt-formula-model-manager/issues

For feature requests, bug reports or blueprints affecting entire ecosystem,
use Launchpad salt-formulas project:

    https://launchpad.net/salt-formulas

Developers wishing to work on the salt-formulas projects should always base
their work on master branch and submit pull request against specific formula.

You should also subscribe to mailing list (salt-formulas@freelists.org):

    https://www.freelists.org/list/salt-formulas

Any questions or feedback is always welcome so feel free to join our IRC
channel:

    #salt-formulas @ irc.freenode.net
