# Copyright 2020 Google LLC
# 
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
# 
#     https://www.apache.org/licenses/LICENSE-2.0
# 
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

SHELL := bash

# IMPORTANT
# - This will be the entrypoint when building the docker image.
.gen/docker-image: .gen/new-image-id
	NEW_ID=$$(cat .gen/new-image-id | cut -d ':' -f 2); if [[ "$${NEW_ID}" != $$(cat $@ 2>/dev/null) ]]; then echo "$${NEW_ID}" > $@; fi

.gen/new-image-id: .FORCE
	docker build image --iidfile $@

.PHONY: .FORCE
.FORCE:
