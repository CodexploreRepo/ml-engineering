- Meta Data:
- Kubeflow: also provide Meta checking but a wrapper on Meta Data management on top of TFX
  - run top of of Kubernetes system
  - need to have kubernestest cluster 
  - open-source, so it can run anywhere

- Kubeflow Pipelines platform consists of:
  - A user interface (UI) for managing and tracking experiments, jobs, and runs.
  - An engine (Orchestration) for scheduling multi-step ML workflows.
  - An SDK (python SDK) for defining and manipulating pipelines and components.
  - Notebooks for interacting with the system using the SDK.

In this example, we already have the container, so we just need a wrapper function to return the information 
- First function: is to download something
- SEcond Function: is to do 
<img width="750" alt="Screenshot 2022-06-14 at 19 57 16" src="https://user-images.githubusercontent.com/64508435/173571628-df8beb52-6db1-4ffb-97db-bf75868e7e46.png">
<img width="750" alt="Screenshot 2022-06-14 at 19 57 58" src="https://user-images.githubusercontent.com/64508435/173571748-ebfb4e96-3fb4-4c56-abdb-4973fa85d027.png">

- Concat these 2 container togethers
  - Output for first task is the input for the second tasks

<img width="750" alt="Screenshot 2022-06-14 at 19 58 41" src="https://user-images.githubusercontent.com/64508435/173571860-ec0ae8d9-52f1-4c7f-91b2-05ce1d1f2ddd.png">

- Python function as component (not recommend) as we need to build that again when other people is used.
- <img width="764" alt="Screenshot 2022-06-14 at 20 35 33" src="https://user-images.githubusercontent.com/64508435/173578292-86ae98c0-df61-4017-9fcb-5a2900d0eef0.png">


- KFP

```Python
pip install kpf
```
- Kubeflow Pipeline SDK V1 -> Kubeflow Pipeline
- Kubeflow Pipeline SDK V1 -> Kubeflow Pipeline and Vertex AI Pipeline

# TFX
- TFX (only use for buidling ML pipeline) and providing multiple component
- TFX is a platform for building and managing ML workflows in a production environment


# Meta Data
- artifact: could be dataset, model, prediction, log
- MLflow: 
