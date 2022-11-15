ARG RELEASE
FROM ghcr.io/dbt-labs/dbt-snowflake:${RELEASE}

# [Optional] Allow the vscode user to pip install globally w/o sudo
# ENV PIP_TARGET=/usr/local/pip-global
# ENV PYTHONPATH=${PIP_TARGET}:${PYTHONPATH}
# ENV PATH=${PIP_TARGET}/bin:${PATH}
# RUN mkdir -p ${PIP_TARGET} \
#     && chown vscode:root ${PIP_TARGET} \
#     && echo "if [ \"\$(stat -c '%U' ${PIP_TARGET})\" != \"vscode\" ]; then chown -R vscode:root ${PIP_TARGET}; fi" \
#         | tee -a /root/.bashrc /home/vscode/.bashrc /root/.zshrc >> /home/vscode/.zshrc

# [Optional] If your pip requirements rarely change, uncomment this section to add them to the image.
COPY requirements.txt /tmp/pip-tmp/


# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends g++ unixodbc-dev python3-dev libssl-dev libffi-dev git ssh-client gnupg software-properties-common curl

# [Optional] Uncomment this section to install Terraform
RUN curl -fsSL https://apt.releases.hashicorp.com/gpg | apt-key add -
RUN apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
RUN apt-get update && apt-get install terraform


RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
   && rm -rf /tmp/pip-tmp
