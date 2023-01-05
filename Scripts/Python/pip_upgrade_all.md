On Linux, you can directly run 

```bash
wget -O - https://raw.githubusercontent.com/realKarthikNair/realKarthikNair/main/scripts/pip_upgrade.py | python
```

Or (e.g. on windows, or if you want to inspect the script)

```python
#!/usr/bin/python
import pkg_resources
from subprocess import call

packages = [dist.project_name for dist in pkg_resources.working_set]
call("pip install --upgrade " + ' '.join(packages), shell=True)
``` 