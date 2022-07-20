
## ansible install nginx on localhost

- in the cfg file create [local] group with localhost
- in [local:vars] set `ansible_conneciton=local`
and
 run `ansible-playbook -i inventory.cfg local -b`
___

## ansible install nginx on aws

- in the cfg file create [aws] group with your aws host
- in [aws:vars] set your aws user and key location
and run `ansible-playbook -i inventory.cfg aws -b`<br/>
note: yum installs require python2<br/>
with EC2 [epel-release](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-enable-epel/) is missing
___

## ansible install nginx on a container
linux or nginx containers don't come with ssh built in and configured a `Dockerfile` of composition is needed to automate ssh installation, configuration and ssh authorization.
