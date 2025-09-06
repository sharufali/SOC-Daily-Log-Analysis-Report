
# 🔍 Splunk Firewall Log Analysis – Day 1

## 📌 Log Entry Analyzed
```
29/08/2017 15:11:37.000
Aug 29 04:11:37 10.0.1.1  1,2017/08/29 04:11:36,009401015183,TRAFFIC,end,1,2017/08/29 04:11:36,10.0.1.200,52.40.10.231,71.39.18.125,52.40.10.231,Inside-Outside,,,incomplete,vsys1,Inside,Outside,ethernet1/2,ethernet1/1,Jupiter,2017/08/29 04:11:36,5576,1,40462,443,56945,443,0x40001b,tcp,allow,134,74,60,2,2017/08/29 04:11:31,0,any,0,2538635,0x0,10.0.0.0-10.255.255.255,US,0,1,1
```

---

## 📝 Key Findings from the Log

- **Timestamp:** `Aug 29 04:11:37`  
- **Firewall IP:** `10.0.1.1`  
- **Log Type:** `TRAFFIC`  
- **Private Source IP:** `10.0.1.200`  
- **Translated Source IP (NAT):** `71.39.18.125`  
- **Destination IP:** `52.40.10.231 (US IP Range)`  
- **Direction:** `Inside → Outside` (inbound to outbound traffic)  
- **Source Port:** `40462` (random/private port)  
- **Translated Source Port:** `56945`  
- **Destination Port:** `443 (HTTPS)`  
- **Protocol:** `TCP`  
- **Firewall Action:** `ALLOW`  
- **Bytes Processed:** `134 (total), 74 outbound, 60 inbound`  
- **Destination Country:** `US`

---

## 🛠️ Step-by-Step Learning

### 🔹 Step 1: Internal IP
- Example: `10.0.1.200`  
- Private IP (cannot travel directly on internet).  

### 🔹 Step 2: NAT (Network Address Translation)
- Firewall translates private IP → public IP.  
- `10.0.1.200` → `71.39.18.125`  

### 🔹 Step 3: Internet Communication
- Outside world sees only the **public IP**.  
- Server replies to `71.39.18.125`, not the internal IP.  

### 🔹 Step 4: Firewall Mapping
- Firewall NAT table maps:  
  `71.39.18.125 ↔ 10.0.1.200`  
- Ensures response goes back to the correct internal system.  

✅ **Analogy:**  
Internal IP = Apartment number  
Public IP = Building’s main gate  
Firewall = Security guard keeping track of who ordered food  

---

## 📊 Important Log Fields

| Field | Example | Description |
|-------|---------|-------------|
| Source IP | 10.0.1.200 | Internal/private IP |
| Destination IP | 52.40.10.231 | External server |
| Translated Source IP | 71.39.18.125 | NAT public IP |
| Source Port | 40462 | Random/private port |
| Destination Port | 443 | HTTPS |
| Translated Source Port | 56945 | NAT-assigned port |
| Timestamp | Aug 29 04:11:37 | Event time |
| Action | Allow | Firewall decision |
| Bytes | 134 (total) | Data processed |
| Country | US | Destination country |

---

## 📷 Screenshots

I have attached my handwritten notes and Splunk diagrams for better understanding:  
- Firewall Logs vs Traffic Logs  
- NAT Translation Example  
- Important Fields in Logs  

---

## 🎯 Conclusion

Today I learned how **firewalls log NAT translations and traffic flows** in Splunk.  
- Source IPs from private ranges are translated before reaching the internet.  
- Ports are dynamically assigned and translated.  
- Firewall logs provide crucial visibility into **who accessed what, when, and how**.  

