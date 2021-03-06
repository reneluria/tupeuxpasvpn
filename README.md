TuPeuxPasVPN
============

On-demand ansible provided VPN endpoint, using aws ec2 and sshuttle

Dependencies
------------

* ansible https://docs.ansible.com/
* boto https://pypi.org/project/boto/
* ssh 
* sshuttle https://github.com/sshuttle/sshuttle

Installation
------------

Nothing to install if deps are already met.

Otherwise:

```
pipenv shell
```

or

```
python3 -m venv venv
. venv/bin/activate
python3 -m pip install -U pip wheel
python3 -m pip install -r requirements.txt
```

Usage
-----

To create an ssh endpoint in London:

```
SSH_AUTH_SOCK= ansible-playbook create-instance.yml -e 'region=eu-west-2'
```

It creates a vm in the given ec2 region and adds it to inventory.

It also creates a helper script in `artifacts` folder.

Launch VPN like this:

```
./artifacts/start-vpn.sh
```

And in another terminal you can check where you apparently are:

```
$ curl ipinfo.io
{
  "ip": "3.8.174.42",
  "hostname": "ec2-3-8-174-42.eu-west-2.compute.amazonaws.com",
  "city": "London",
  "region": "London, City of",
  "country": "GB",
  "loc": "51.5115,-0.0912",
  "postal": "EC4R",
  "org": "AS16509 Amazon.com, Inc."
}
```

And remove this instance when you're done:

```
ansible-playbook delete-instance.yml -e 'region=eu-west-2'
```

Notes
-----

* This recipe generates a ssh keypair for this purpose

* The VM is created with a security group allowing only your public ip to connect to it

* You need to set your aws cli config or EC2_ACCESS_KEY and EC2_SECRET_KEY variables

* Feel free to adapt the template of the vpn script to make it less verbose and daemonize for example

Author
------

Rene Luria