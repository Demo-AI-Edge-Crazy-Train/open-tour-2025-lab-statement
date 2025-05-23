+++
title = "Test services"
draft = false
weight = 9
+++

Nous allons simuler le fonctionnement du train :
1. Ouverez un nouveau terminal
![terminal](/images/dev-section/new-terminal-bash.png)
2. Executez la commande ci-dessous pour récupérer l'URL de la console de monitoring :  
```
oc get routes -o jsonpath='{range .items[*]}{.metadata.annotations.che\.routing\.controller\.devfile\.io/endpoint-name}{"\t"}http://{.spec.host}{"\n"}{end}' | grep monitoring-svc | cut -f 2
```
![URL monitoring](/images/dev-section/get-url-monitoring.png)

3. Copiez l'URL, lancez une nouvelle fênetre de votre navigateur en mode anonyme (afin d'avoir un cache vide), insérez l'URL.

![URL monitoring](/images/dev-section/monitoring-console.png)

{{% notice warning %}}
**Google Chrome** semble transformer l'URL HTTP en URL HTTP**S**.
Si vous obtenez un message d'erreur disant *"Application is not available. The application is currently not serving requests at this endpoint. It may not have been started or is still starting."*, vérifiez le schéma de l'URL (HTTP/HTTPS) ou ouvrez l'URL à l'aide d'un autre navigateur.
Firefox semble fonctionner parfaitement pour cette utilisation.
{{% /notice %}}

4. Retournez à votre terminal et exécutez la commande suivante :
```
curl -X 'POST'   'http://localhost:8082/capture/test' -H 'accept: */*'
```

5. A partir de votre navigateur vous devriez visualiser en temps réel la simulation du train et la détéction des panneaux de signalisation. Si la vidéo ne démarre pas, actualisez votre navigateur.

![streaming video](/images/dev-section/streaming-video.png)

Bravo ! la simulation a bien fonctionné :) maintenant vous pouvez arrêter la simulation en fermant tous les terminaux.