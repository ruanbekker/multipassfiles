.PHONY: list
prepare:
	sed -i '' "s|SSH_PUBLIC_KEY_STRING|`cat ~/.ssh/id_rsa.pub`|g" ./cloud-init.yml

deploy:
	multipass launch bionic --name go-env --cpus 1 --mem 512m --disk 1G --cloud-init cloud-init.yml

destroy:
	multipass delete --purge go-env

list:
	@$(MAKE) -pRrq -f $(lastword $(MAKEFILE_LIST)) : 2>/dev/null | awk -v RS= -F: '/^# File/,/^# Finished Make data base/ {if ($$1 !~ "^[#.]") {print $$1}}' | sort | egrep -v -e '^[^[:alnum:]]' -e '^$@$$'
