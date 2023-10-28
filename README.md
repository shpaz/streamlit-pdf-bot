# streamlit-pdf-bot
This repository contains all the relevant information regarding the creation of a ChatBot based on ChatGPT and Azure Cognitive Services. This bot will act as a virtual assistant for end users, and will be accessible 24/7 for all their needs (mainly for analyzing PDF documents).

## Deploying On Openshift 

In order to deploy this demo on an Openshift cluster, make sure to first create a new project: 

```bash 
$ oc new-project streamlit-pdf-bot
``` 

After that, as `ChromaDB` is using privileged escalation containers, we'll have to change the `SCC` to `anyuid` just for the sake of this PoC. 
*Note!* Important to say, this is not recommended in production as it's a security breach. In a real environment, you'll have to pick and choose the proper image, or create a suitable service account: 

```bash   
$ oc adm policy add-scc-to-user anyuid -z default
``` 

Now, let's deploy the application itself: 

```bash 
$ oc apply -f openshift/
``` 

## Building The Streamlit App 

In order to build the Streamlit container, we'll have to first swtich the directory: 

```bash
$ cd src/
```

Now, you can build the image using the Containerfile you have in the `src` directory: 

```bash
$ podman build -t <image_name .
```


