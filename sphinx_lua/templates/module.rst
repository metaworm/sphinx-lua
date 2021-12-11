.. lua:module:: {{ module.name }}

{{ module.short_desc|process_link if module.short_desc }}

{{ module.desc|process_link if module.desc }}

{% if module.usage -%}
**Usage:**

.. code-block:: lua
    :linenos:

    {{ module.usage|indent(4) }}
{%- endif %}

{% if module.data %}
Variables
==========

.. list-table::
    :align: left
    :header-rows: 1

    * - Name
      - Type
      - Desc
{% for data in module.data %}
    * - {{ data.name }}
      - {% with type=data.type %} {% include "type.rst" %} {% endwith %}
      - {{ data.short_desc }} {{ data.desc }}
{% endfor %}
{% endif %}

{% if module.functions %}
Functions
==========

.. list-table::
    :align: left

{% for function in module.functions %}
    * - `{{ function.name}}({{ function.params|join(', ', attribute='name') }}) <#{{ module.name+'.'+function.name }}>`_
      - {{ function.short_desc }}
{% endfor %}
{% endif %}

{% if module.classes %}
Classes
==========

{% for model in module.classes %}

`{{ model.name }} <#{{ module.name+'.'+model.name }}>`_
-------------------------------------------------------

{{ model.short_desc }}

{% if model.methods %}
.. list-table::
    :align: left
{% for method in model.methods %}
    * - `{{ method.name }}({{ method.params|join(', ', attribute='name') }}) <#{{ module.name+'.'+model.name+'.'+method.name }}>`_
      - {{ method.short_desc }}
{% endfor %}
{% endif %}

{% endfor %}
{% endif %}

Details
==========

{% for function in module.functions %}
{% include "function.rst" %}
{% endfor %}

{% for model in module.classes %}
{% include "class.rst" %}
{% endfor %}
