# python-docker-management
A set of python scripts, intended to manage bunch of simple stateless services like proxies and VPNs

## Main goal
Simplify management of tons of look-the-same containers without using heavyweight tools like Kubernetes.

### Live case
I am an operator of proxies and VPNs, which are used by people in oder to circumvent government-influenced censorship. So, I need to run the same tools against 
slightly different configs. I need to do this on various hosts, because some host could be banned in target audience jurisdiction. Moreover, I need to do it quick 
in order to minimize downtime.

Most tools could be configured "automagically" and provide output as link, sufficient to use in client software (Telegram and Outline deeplinks). So, I want to 
avoid typing long commands like
```docker run -d -p 80:8080 -e SECRET=0000```

The main tool simplifies this to short commands like `docker-managed-port-instances start MTProxy`, producing readable JSON output, allow to limit port range, which 
could be used on host, and make using dockered servers quick and comfortable

## Prerequisites
I am fan of Ubuntu, so keep in mind that I targeted on Ubuntu 16.04 and 18.04. Don't forget to refresh repos
```sudo apt-get -y apt-get update```
So, on 18.04 and more fresh you need to install python 2.7, because them packed with python 3.x by default.
```sudo apt-get -y install python```
After that you could clone this repo, and allow script to be runnable
```
sudo chmod +x ./docker-managed-port-*
sudo chmod +x ./*-link
```
Finally, you run the main script, which do the rest of work
```sudo ./docker-managed-port-instances init```

## Strange things
The "package descriptors" are built-in into main script. Yes, it's ugly, but make it self-contained and self-sufficient - feel free to extend this list.
Code itself not perfect and clean, I know. 
Some aspects in `docker-managed-port-server` are subjects of improvement and TBD - authentication tokens in particular.

## And what?
Run `./docker-managed-port-instances` and see built-in help.

##Ok, I'd forget which links I used on my host
```./docker-managed-port-server &
curl -sS http://localhost:5000/deeplinks```
