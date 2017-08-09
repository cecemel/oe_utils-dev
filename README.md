# oe_utils-dev

## deployment of dev environment for oe_utils

### build instructions

#### assumes
- access to OE private repos
- osx/linux environment
- docker installed
- python installed
- git
- pycharm enterprise edition

#### general setup
```
# assumes you have access to OE private repos
git clone --recursive https://github.com/cecemel/oe_utils-dev.git
cd oe_utils-dev
```

### building & running
```
# assumes you are in folder oe_utils-dev
docker-compose stop; docker-compose rm -f; #not required, but cleans your working environment
# assumes you are in metaaldetectievondstmeldingen-dev
python build_images.py [GITHUB_USER] [GITHUB_PASS];
docker-compose up; # note in this case only dependent services will keep running.
```

#### reset backend one liner
```
docker-compose stop; docker-compose rm -f; rm -rf data/*; python build_images.py [GITHUB_USER] [GITHUB_PASS]; python migrate_dbs.py; python init_data.py;
```

### running in pycharm
see e.g. 
https://blog.jetbrains.com/pycharm/2017/03/docker-compose-getting-flask-up-and-running/

### rebuilding (when e.g. requirements.txt has been updated)
```
# e.g.
python build_images.py [GITHUB_USER] [GITHUB_PASS] oe_utils
```

### caveats-todos
- test.ini is a little hackish -> it is mounted from docker-files/oe_utils/test.ini (to account for networkning issues)
- if you get error HTTPError similar to: "401 Client Error: Unauthorized for url": restart your docker daemon
- scripts contain some hard coded parameters and should be cleaned
- a generic base image should be extract to speed up image build
- clean-up scripts, docker-compose should be sufficient for all migrations
- for some mysterious reason, pycharm kills the containers when running the unittests for the first time. 
    So you have to run them a second time and it should be fine from then on. (to get dependent services started)
