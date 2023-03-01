#
# Makefile: Watson Speech-To-Text WSTT
#

# Checks required environment variables
-include ../env.check.mk

all: publish-runtime deploy-policy

publish-runtime:
	make -C src/runtime build-image
	make -C src/runtime push-image
	make -C src/runtime publish-service

deploy-policy:
	make -C src/runtime deploy-policy
