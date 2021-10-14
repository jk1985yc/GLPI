# GLPI
docker-compose with Nginx MySQL.

### "Checking write permissions for setting files" Error
```
chmod -R 777 config files marketplace
```

### DB connection using container name

### Fusioninventory Plugin Agent use
Amend agent folder "etc/agent.cfg"
```
...
server = http://$IPor$DomainName:$Port/plugins/fusioninventory/
...
```

Refer  
https://github.com/fusioninventory/fusioninventory-for-glpi/releases  
https://github.com/fusioninventory/fusioninventory-agent/releases  
