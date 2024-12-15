---
description: To setup Ollama with Open WebUI LXC
---

# Open WebUI LXC

## 1/ Change LXC default port

### **Identify the process using port 8080**

```bash
ps aux | grep 8080
```

{% code title="example output" overflow="wrap" %}
```
root 7967 0.0 14.5 2630104 609120 ? Ssl 00:40 0:07 /usr/bin/python3 /usr/local/bin/uvicorn open_webui.main:app --host 0.0.0.0 --port 8080 --forwarded-allow-ips * root 8388 0.0 0.0 6332 1120 pts/3 S+ 00:44 0:00 grep 8080
```
{% endcode %}

### Locate the process directory

Navigate into the container (e.g. 100).

```bash
pct enter 100
```

Search entire filesystem for the directory named `open_webui`.

```bash
find / -type d -name "open_webui"
```

{% code title="example output" overflow="wrap" %}
```
root@openwebui:~# find / -type d -name "open_webui" /opt/open-webui/backend/open_webui find: ‘/sys/kernel/debug’: Permission denied
```
{% endcode %}

### Modify the startup command

Navigate to the directory where `open_webui` is located.

```
cd /opt/open-webui/backend/open_webui
```

Locate the application startup file.

```
grep -r "uvicorn" .
```

{% code title="example output" overflow="wrap" %}
```
root@openwebui:/opt/open-webui/backend/open_webui# grep -r "uvicorn" .
./__init__.py:import uvicorn
./__init__.py:    uvicorn.run(open_webui.main.app, host=host, port=port, forwarded_allow_ips="*")
./__init__.py:    uvicorn.run(
./config.py:logging.getLogger("uvicorn.access").addFilter(EndpointFilter())
grep: ./__pycache__/__init__.cpython-311.pyc: binary file matches
grep: ./__pycache__/config.cpython-311.pyc: binary file matches
root@openwebui:/opt/open-webui/backend/open_webui# 
```
{% endcode %}

Navigate to the application configuration file.

{% code overflow="wrap" %}
```bash
nano /opt/open-webui/backend/open_webui/__init__.py
```
{% endcode %}

Modify the port variable.

{% code overflow="wrap" %}
```python
uvicorn.run(open_webui.main.app, host=host, port=4010, forwarded_allow_ips="*")
```
{% endcode %}

Restart the application.

```bash
pct stop 100 
pct start 100
```

### Update the Python path to include the correct directory.

Set the Python path manually by running the following command:

```bash
export PYTHONPATH=$PYTHONPATH:/opt/open-webui/backend
```

Run the application manually again after setting the `PYTHONPATH`:

{% code overflow="wrap" %}
```bash
/usr/bin/python3 /usr/local/bin/uvicorn open_webui.main:app --host 0.0.0.0 --port 4010 --forwarded-allow-ips *
```
{% endcode %}

### Verify the change

```bash
http://<ip-address>:4010
```

