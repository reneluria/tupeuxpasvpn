TuPeuxPasVPN
============

On-demand ansible provided VPN endpoint, using aws ec2 and sshuttle

Dependencies
------------

* ansible https://docs.ansible.com/
* boto https://pypi.org/project/boto/
* ssh 
* sshuttle https://github.com/sshuttle/sshuttle

Usage
-----

To create an ssh endpoint in London:

```
ansible-playbook create-instance.yml -e 'region=eu-west-2'
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

ansible-playbook delete-instance.yml -e 'region=eu-west-2'


Think of adapting the variables at the start of the playbook to match your ssh public key

Author
------

Rene Luria