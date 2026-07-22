# Testbed 3
## Table Of Contents
- [Scenario](#scenario)
- [Step](#step)
- [Mitigation](#mitigation)
- [DEMO Video](#demo-video)

## Scenario

<div align="center">
<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/920e694f-aa80-4333-af2e-53d9d8940413" />
</div>


## Step

### gNB Configuration
> ```
> Bandwidth: 40 MHz (106 PRB, SCS 30 kHz)
> Center frequency: 3619.2 MHz 
> PRACHConfigurationIndex: 159
> msg1_FDM = ONE
> ```

Make sure your config:

file path: `/openairinterface5g/targets/PROJECTS/GENERIC-NR-5GC/CONF/gnb.sa.band78.fr1.106PRB.usrpb210.conf`

<img width="632" height="323" alt="image" src="https://github.com/user-attachments/assets/ea5fcbdf-fc19-4b2c-9d61-0197888f7e22" />

### Deploy ROMF
> ```
> # SMO
> cd ~/kevin/RAN-OAM-Mediation-Function
> ./redeploy.sh
> ```
### Deploy rapp
> ```
> # SMO
> cd ~/kevin/rapp-mitigation
> ./redeploy.sh
>
> # then you can see log by k9s or command:
> kubectl logs -f -n $NAMESPACE -l $APP_LABEL
> ```

### check log by k9s
> ```
> # SMO
> k9s
> 
> # then search "rapp" and press "enter" via:
> /rapp
> 
> # go to "kevin-mitigation-rapp-dev-7b95ff445f-x5d8c" by press "l" (log)
> ```

### Start gNB
> ```
> # oaignb
> 
> cd ~/openairinterface5g/cmake_targets/ran_build/build
> sudo ./nr-softmodem -O ../../../targets/PROJECTS/GENERIC-NR-5GC/CONF/gnb.sa.band78.fr1.106PRB.usrpb210.conf  \
>     --gNBs.[0].min_rxtxtime 6 \
>     -E \
>     --continuous-tx \
>     --log_config.PRACH_debug \
>     --telnetsrv \
>     --telnetsrv.shrmod o1 \
>     2>&1 | awk '{ cmd = "date +\"[%Y-%m-%d %H:%M:%S.%3N]\""; cmd | getline ts; close(cmd); print ts, $0; fflush(); }' > ~/kevin.log   #The file you save log
> ```

### Start o1 Adapter
> ```
> # oaignb
> 
> cd ~
> ./execute_o1_adapter.sh 
> ```

### Start MTK UE
[Tutorial](../MTK_UE.md)


### Start Attacker
> ```
> # oaiue
>
> cd OAI-UE-MSG1-attacker/cmake_targets/ran_build/build/
> sudo ./nr-uesoftmodem -r 106 --numerology 1 --band 78 -C 3619200000 --ssb 516 -E --ue-fo-compensation
> ```

## Mitigation 

<img width="1210" height="626" alt="image" src="https://github.com/user-attachments/assets/6c70a78a-9fb5-4e92-9e12-5017bb6a4986" />

When rapp analyze the attack is taking action, it will update:
- `PRACH_Configuration`: 148
- `absoluteFrequencySSB`: 621312
- `dl_absoluteFrequencyPointA`: 620040
So the attacker can't find gNB due to it's center frequency is`-C 3619200000`.

Then we need to lock the UE frequency to 621312.

So it can be connect to the gnb after mitigation.

### After Mitigation
Is important to close all gnb while you finish.
> ```
> ./kill_gnb.sh 
> ```


### [DEMO Video](https://youtu.be/DQgDfQ9bDjM)
