## Attacker test with webUI
## Table Of Contents
- [Attacker test with webUI](#attacker-test-with-webui)
- [Table Of Contents](#table-of-contents)
- [Step](#step)
  - [1. Redeploy webUI](#1-redeploy-webui)
  - [2. Redeploy ROMF](#2-redeploy-romf)
  - [3. Redeploy rapp](#3-redeploy-rapp)
  - [4. Open webUI](#4-open-webui)
  - [5. Open AnyDesk](#5-open-anydesk)
  - [DEMO Video (YouTube)](#demo-video-youtube)


## Step
### 1. Redeploy webUI
```bash
# SMO

cd ~/richard/tool-demo
./redeploy-v3.sh  
```

### 2. Redeploy ROMF
```bash
# SMO

cd ~/kevin/RAN-OAM-Mediation-Function 
./redeploy.sh   
```

### 3. Redeploy rapp
```bash
# SMO

cd ~/kevin/rapp-mitigation     
./redeploy.sh   
```
> When all redeployment finish, open k9s or use command:
```bash
kubectl logs -f -n nonrtric -l app=kevin-mitigation-rapp-dev
```


### 4. Open webUI
[Link](http://192.168.8.69:30532/)

### 5. Open AnyDesk

### [DEMO Video (YouTube)](https://youtu.be/OPG5lpVmrOU)
