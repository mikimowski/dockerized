FROM jupyter/scipy-notebook

LABEL description="JupyterLab Env"

#RUN pip install --upgrade jupyterlab

RUN conda install --quiet --yes -c conda-forge xeus-python
RUN conda install --quiet --yes -c conda-forge plotly
# Language server
RUN conda clean --all -f -y

# this one requires setting up in config...
RUN pip install --quiet jupyterlab_execute_time
RUN pip install --quiet lckr-jupyterlab-variableinspector

# themes
RUN pip install --quiet jupyterlab_theme_solarized_dark

RUN pip install --quiet jupyter-offlinenotebook
RUN pip install --quiet -U kaleido
# Language server
RUN pip install --quiet jedi==0.17.2
RUN pip install --quiet python-language-server
RUN pip install --quiet jupyterlab-lsp
RUN pip install --quiet pydocstyle pycodestyle mccabe pyflakes pylint rope yapf autopep8

# install code formatter
RUN pip install --quiet jupyterlab_code_formatter isort black

# install Jupyter Lab extensions you need
RUN jupyter labextension install jupyterlab-plotly --no-build
RUN jupyter labextension install jupyter-offlinenotebook --no-build
RUN jupyter labextension install '@krassowski/jupyterlab-lsp@3.4.1' --no-build

# themes
RUN jupyter labextension install jupyterlab-theme-solarized-dark --no-build
RUN jupyter labextension install @arbennett/base16-nord --no-build
RUN jupyter labextension install @arbennett/base16-mexico-light --no-build
RUN jupyter labextension install @arbennett/base16-solarized-dark --no-build
RUN jupyter labextension install @arbennett/base16-monokai --no-build

# Pytorch
RUN pip install --quiet torch==1.8.0+cpu torchvision==0.9.0+cpu torchaudio==0.8.0 -f https://download.pytorch.org/whl/torch_stable.html

# build jupyter lab and clean-up
RUN set -ex \
   && jupyter lab build --dev-build=False --minimize=False -y \
   && jupyter lab clean -y \
   && rm -rf "/home/${NB_USER}/.cache/yarn" \
   && rm -rf "/home/${NB_USER}/.node-gyp" \
   && fix-permissions "${CONDA_DIR}" \
   && fix-permissions "/home/${NB_USER}"
