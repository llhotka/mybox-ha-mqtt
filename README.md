# MyBox integration to Home Assistant via MQTT

This repository contains annotated configuration of MQTT-based
sensors and scripts that can be used for integrating a
[MyBox](https://mybox.eco/produkty-kategorie/nabijeci-stanice)
wallbox to Home Assistant.

A step-by-step procedure for integrating a MyBox wallbox to Home
Assistant is described in this [blog post](https://blog.lhotka.name/posts/mybox-home-assistant).

The master file [mybox-ha-mqtt.org](./mybox-ha-mqtt.org) is written in
the Emacs [Org mode](https://orgmode.org) syntax and uses its literate
programming capabilities for generating (“tangling”) the following
YAML configuration files:

* `mqtt.yaml` – MQTT-based sensors and binary sensors
* `scripts.yaml` – scripts for controlling the wallbox
* `customizations.yaml` – customization of the energy meter

For convenience, the generated files are also present in this
repository. They are supposed to be included in Home Assistent
configuration by adding the following lines to the main configuration
file `configuration.yaml`:

``` yaml
homeassistant:
  customize: !include customizations.yaml

mqtt: !include mqtt.yaml
script: !include scripts.yaml
```

If these files already exist in Home Assistant configuration, the
contents of generated files have to be merged into them.

> [!IMPORTANT]
> MQTT topics in YAML definitions use placeholders DEVICE_ID and
> ROOT_TOPIC. These should be replaced by the actual device ID and
> configured MQTT root topic.

In order to enjoy the full comfort of the Org mode, the master file
should be edited in Emacs. The three configuration files can then be
generated by using Emacs function `org-babel-tangle` (keyboard
shortcut `C-c C-v t`).

Support for editing YAML in source code blocks can be added by
installing

1. [YAML mode](https://github.com/yoshiki/yaml-mode),
   e.g. from [MELPA](https://stable.melpa.org/#/yaml-mode)
2. my emacs-lisp module
   [ob-yaml.el](https://github.com/llhotka/ob-yaml) that enables
   YAML mode in source code blocks. 

GitHub now understands Org mode syntax almost perfectly, so nicely rendered
[master file](mybox-ha-mqtt.org) can also be viewed directly in the
GitHub repo.
