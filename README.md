## Haaukins Documentation Hub

- This repository will inclued all recent documentation and information regarding to Haaukins project. All information will be added and updated in time manner frequency.

### How to run 

It can be run using Docker with following command; 

```bash 

$ docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll  -it -p 4000:4000 jekyll/jekyll bundle exec jekyll serve

```

Note, docker command should be executed under root path of the project where `_config.yml` file is exist.  Another important point is that, `$(pwd)` should be changed on Windows OS with equivalent of it. 
