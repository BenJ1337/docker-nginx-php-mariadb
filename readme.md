# Docker-Compose workspace to develope redaxo CMS

## Setup
###  Clone redaxo
```
https://github.com/redaxo/redaxo.git
```
### Configure file permission for www-user inside the php container
Edit the group id in `php-fpm/Dockerfile` to the group id which is set in the cloned redaxo directory and it's subdirectories.

## Run

```
docker-compose up
```

### Optionally debugging with xDebug
1. Install the Extension https://marketplace.visualstudio.com/items?itemName=xdebug.php-debug
2. Start the xDebug Debugger
3. Add breakpoints in CSCode
4. Start a HTTP Request