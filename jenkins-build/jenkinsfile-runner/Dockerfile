# Copyright 2021 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

ARG baseImage=apigee/devrel-jenkins-base
ARG baseImageTag=latest

FROM jenkins4eval/jenkinsfile-runner:1.0-beta-29 as filerunner

FROM ${baseImage}:${baseImageTag}

USER root
WORKDIR /usr/share/jenkins
RUN jar -xvf jenkins.war
USER jenkins

COPY --from=filerunner --chown=jenkins /app /app
WORKDIR /app/jenkins

ENTRYPOINT ["/app/bin/jenkinsfile-runner", "-w", "/usr/share/jenkins/", "-p", "/usr/share/jenkins/ref/plugins", "-f"]

CMD ["/workspace/Jenkinsfile"]
