## OCUDU attack test
## Table Of Contents
- [OCUDU attack test](#ocudu-attack-test)
- [Table Of Contents](#table-of-contents)
- [Scenario](#scenario)
- [Step](#step)
  - [1.Start the gNB](#1start-the-gnb)
  - [2.Start Attacker](#2start-attacker)
  - [Results](#results)
  - [DEMO Video](#demo-video)

## Scenario
```bash
gNB: OCUDU gNB (release_26 6a7afc6c1b)

band n78
20 MHz
SCS = 30 kHz
RB (Resourse Block) = 51
center freq = 3619200000 (3.6192 GHz)
```
```mermaid
graph TD
    %% Define Styles
    classDef host fill:#2ca02c,stroke:#1b5e20,stroke-width:2px,color:#fff;
    classDef proc fill:#1f77b4,stroke:#0d47a1,stroke-width:2px,color:#fff;
    classDef sdr fill:#ff7f0e,stroke:#e65100,stroke-width:2px,color:#fff;
    classDef target fill:#d50000,stroke:#b71c1c,stroke-width:2px,color:#fff;

    subgraph Attacker_Node ["Attacker Node (Ubuntu Host)"]
        Host["Ubuntu 24.04 LTS Host"]:::host
        Process["Msg1 Attacker Process<br/>(2026 w26)"]:::proc
        UHD["UHD Driver (SDR Interface)"]:::proc
        
        Host --- Process
        Process --- UHD
    end

    USRP["USRP B210"]:::sdr
    gNB["OCUDU<br/>(release_26 6a7afc6c1b)"]:::target

    %% 備註：因 B210 僅支援 USB 介面，此處的標籤可視需求簡化為 USB，或保留原始樣式。
    UHD --- |"USB 3.0"| USRP
    USRP --- |"Uu Interface"| gNB
```

## Step 

### 1.Start the gNB
[config](./config/OCUDU_config.txt)
```bash
# oaignb

cd ~/ocudu/build/apps/gnb
sudo ./gnb -c gnb_rf_b200_tdd_n78_20mhz.yml

```

### 2.Start Attacker
```bash
# oaiue

cd OAI-UE-MSG1-attacker/cmake_targets/ran_build/build/
sudo ./nr-uesoftmodem -r 51 --numerology 1 --band 78 -C 3619200000 --ssb 42 -E --ue-fo-compensation --seq 3 --ue-txgain 0
```

### Results

### [DEMO Video](https://youtu.be/oIUZ0zYyGtk)
  
---

- **OCUDU preamble detection** mechanism uses the **average energy** within a window **as the threshold** (if the rate : **preamble energy / threshold > 1**, preamble will be detected).
- So if the number of preamble is too much, then the threshold will be much larger, so the preamble is getting hard to be detected.
- If we set the paremeter `rx_gain = 76`, then `dBFS = 1.1`.
- But if we set `rx_gain = 1`, then `dBFS = -60`.
