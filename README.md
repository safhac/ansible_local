
## ansible install nginx on localhost
`ansible-playbook -i local_inventory.yml nginx_local_install.yml -b`
___

## ansible install nginx on a container
linux or nginx containers don't come with ssh built in and configured a `Dockerfile` of composition is needed to automate ssh installation, configuration and ssh authorization.
