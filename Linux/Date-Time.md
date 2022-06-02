---
tags: [time, date, datetime, config, linux, sysadmin]
---

#### Get Current Timezone information
```bash
timedatectl
```

#### Get Available Timezones
```bash
timedatectl list-timezones
# OR Use grep to filter the long list of Timezones
timedatectl list-timezones | grep Australia

#Outputs:
#Australia/ACT
#Australia/Adelaide
#Australia/Brisbane
#Australia/Broken_Hill
#Australia/Canberra
#Australia/Currie
#... (more omitted)

```

#### Set Timezone (sudo required)
```bash
sudo timedatectl set-timezone 'Australia/Sydney'
```