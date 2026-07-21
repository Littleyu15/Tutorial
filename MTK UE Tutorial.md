## MTK UE Manual
## Table Of Content
- [Step](#step)


## Step
### 1.Open ELT tool and MTK UE
![alt text](image/image-1.png)
### 2.Start ELT Connection
1. Connect UE to PC and click "OK"

<img width="445" height="104" alt="image" src="https://github.com/user-attachments/assets/74faf224-f465-47fa-ae0d-c4cf5d12a34d" />

<img width="403" height="135" alt="image" src="https://github.com/user-attachments/assets/99a2ca06-0076-4243-80da-2f7f252d24de" />

2. Click “connect” then click “OK”
<img width="441" height="90" alt="image" src="https://github.com/user-attachments/assets/939acc5d-4524-44d7-96c8-7552fbc9af09" />

<img width="475" height="334" alt="image" src="https://github.com/user-attachments/assets/e12167c8-1af0-4539-8693-845eee2306de" />

### Results
<img width="445" height="74" alt="image" src="https://github.com/user-attachments/assets/d921393a-3935-40d0-bf70-36bd9e7d2bcb" />

---

### 3.Lock NR Cell through ELT
1. Enter flight mode
2. Choose Lock NR Cell in command line : MOD_L4C(for SIM1)、MOD_L4C_2(for SIM2)
3. Fill in AT command : AT+EMMCHLCK=1,11,0,==630048==,==0==. 630048 is SSB ARFCN. 0 is PCI.
4. If you don't want to lock cell id then use this AT command : AT+EMMCHLCK=1,11,0,641280
5. Press `send` to activate

### Results
<img width="1113" height="729" alt="image" src="https://github.com/user-attachments/assets/1737feb9-3662-478c-9c86-4fccf1e6670e" />
