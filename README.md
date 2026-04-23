LINKSYS-EA8300-MODDED-OPENWRT

---

🚀 How to Enable the 896MHz Overclock

Even though this firmware supports **896MHz**, OpenWrt defaults to a "Power Save" mode (716MHz). You must manually switch to the **Performance** gear to unlock the full speed.

### Method 1: The Fast Way (Command Line)
SSH into your router (using PuTTY or your terminal) and run this single command:

```
echo performance | tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
```

### Method 2: The Permanent Way (Web Interface)
To make sure the router stays overclocked even after a restart:

1.  Log into **LuCI** (the web interface).
2.  Go to **System** → **Startup**.
3.  Scroll down to the **Local Startup** box.
4.  Paste the following line right **above** the `exit 0` line:
    `echo performance | tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor`
5.  Click **Save**.

---

## 📊 How to Verify it's Working
To prove you are actually running at **896MHz**, run this command in the terminal:

```bash
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
```
* **Success:** You will see `896000`.
* **Stock:** You will see `716100`.



---

### ⚠️ Important Note on Heat
The IPQ4019 is a tough chip, but **896MHz** generates more heat than stock.
* **Keep it ventilated:** Don't stack other devices on top of the router.
* **Check Temp:** Run `cat /sys/class/thermal/thermal_zone0/temp`. If you see `75000` (75°C) or higher while the router is idle, you might need better airflow.
