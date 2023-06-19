# docker-ml-faq-rassa
ML FAQ model demo with rasa &amp; Docker 

![image](https://github.com/harsh4870/docker-ml-faq-rassa/assets/15871000/0c83ad02-565d-4c3e-a172-c6e75af9101a)


#### Init Rasa

```
docker run  -p 5005:5005 -v $(pwd):/app khalosa/rasa-aarch64:3.5.2 init --no-prompt
```

## Result:

```
023-06-19 08:27:42 INFO     rasa.engine.training.hooks  - Restored component 'MemoizationPolicy' from cache.
2023-06-19 08:27:42 INFO     rasa.engine.training.hooks  - Restored component 'RulePolicy' from cache.
2023-06-19 08:27:42 INFO     rasa.engine.training.hooks  - Restored component 'TEDPolicy' from cache.
2023-06-19 08:27:42 INFO     rasa.engine.training.hooks  - Restored component 'UnexpecTEDIntentPolicy' from cache.
Welcome to Rasa! 🤖

To get started quickly, an initial project will be created.
If you need some help, check out the documentation at https://rasa.com/docs/rasa.

Created project directory at '/app'.
Finished creating project structure.
Training an initial model...
The configuration for policies and pipeline was chosen automatically. It was written into the config file at 'config.yml'.
Your Rasa model is trained and saved at 'models/20230619-082740-upbeat-step.tar.gz'.
If you want to speak to the assistant, run 'rasa shell' at any time inside the project directory.
```

#### Train Model 

```
docker run -v $(pwd):/app khalosa/rasa-aarch64:3.5.2 train --domain domain.yml --data data --out models
```

#### Run model 

```
docker run -v $(pwd):/app khalosa/rasa-aarch64:3.5.2 shell
```

## WebChat

```
docker run  -p 5005:5005 -v $(pwd):/app <IMAGE>:3.5.2  run -m models --enable-api --cors "*" --debug
```

#### Build the WebChat UI frontend

```
docker build -t rasa-webchat:v1 -f Dockerfile-webchat .
```

#### Run

```
docker run -p 8080:80 rasa-webchat:v1
```

Open `localhost:8080` in Browser

<img width="1439" alt="Screenshot 2023-06-19 at 12 10 51 PM" src="https://github.com/harsh4870/docker-ml-faq-rassa/assets/15871000/7184fa0c-123d-4719-ac09-b399514d4199">

