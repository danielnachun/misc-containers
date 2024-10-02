FROM ubuntu:latest
USER root
# For security reasons, SSL certificates and timezone database must be installed by host package manager
# libgl1 is needed for the conda-forge mesa CDT for OpenGL support
# libgomp1 is needed for FINEMAP, which is precompiled and breaks with RPATH relocation
# tmate is needed so that SSH access is possible
# curl is needed to bootstrap pixi
RUN apt-get update && apt-get -y install ca-certificates tzdata libgl1 libgomp1 tmate curl

# Use bash as default shell instead of dash
RUN ln -sf /bin/bash /bin/sh

RUN useradd --no-log-init --create-home --shell /bin/bash --uid 1100 --no-user-group jovyan
COPY --chown=jovyan --chmod=755 entrypoint.sh /usr/local/bin/entrypoint.sh

USER jovyan
ENV PYDEVD_DISABLE_FILE_VALIDATION=1
ENV USER=jovyan
WORKDIR /home/jovyan
CMD ["entrypoint.sh"]
