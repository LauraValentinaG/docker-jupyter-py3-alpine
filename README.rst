Docker files
============

Standard Jupyter port 8888 is exposed, map it to your local port.
You can plug your own persistent notebooks as volume to ``/notebooks`` mount.
Example start of the minimal container::

    docker run -d \
        --name jupyter \
        -p 8888:8888 \
        -v ${PWD}:/notebooks \
        pshchelo/alpine-jupyter-minimal-py3

Extending image at run-time
    The entrypoint to image is ``jupyter-notebook`` (not really configurable
    for now) and the server is run under ``root`` user.
    Together with Terminal available in Jupyter server, this gives you
    possibility to run any shell command from inside the container, including
    adding system packages with ``apk add ...``
    or Python packages with ``python3 -m pip install ...``.

alpine-jupyter-minimal-py3
--------------------------

Basic insecure single user Jupyter Notebook server deployment, Python3-based.
Apart from Python stdlib following Python packages are installed:

- notebook
- ipywidgets
- requests

This makes this image already useful for teaching/showcasing
and some development around Web APIs.

alpine-jupyter-sci-py3
----------------------

In addition to the minimal install, next scientific Python packages are added:

- numpy
- pandas
- sympy
- networkx
- plotly (Plot.ly integration, >= 1.9 has offline mode)
- cufflinks

``matplotlib``, ``scipy`` and scikits will be added later
as they require non-trivial build dependencies

TODO
----

- better startup/shutdown behavior, handle signals and arguments

  - dedicated startup script?
  - move default settings to jupyter config file?
