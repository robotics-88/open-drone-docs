# open-drone-docs

This repo contains documentation for the Robotics 88 entire open source drone stack, including open-drone-core, open-drone-server, and open-drone-frontend. View it [here](https://robotics-88.github.io/open-drone-docs).

## setup
```
python -m venv .env
source .env/bin/activate
pip install -r requirements.txt
```
To view changes locally:
```
mkdocs serve
```

To deploy changes:
```
mkdocs gh-deploy
```
This builds and pushes changes to the gh-pages branch, which is what Github Pages hosts.