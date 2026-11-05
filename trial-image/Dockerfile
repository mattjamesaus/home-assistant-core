# Prepared for a controlled trial only; not built or deployed.
FROM ghcr.io/home-assistant/raspberrypi4-64-homeassistant:2026.10.0@sha256:81a67e6f54171961402ed2964d17b2a929ab669b759efad61688b81a8dcd102d
LABEL io.mattjames.google_execute_patch="8c308d887225f99be0475b93f62b3bf62144e88d"
COPY homeassistant/components/google_assistant/helpers.py /usr/src/homeassistant/homeassistant/components/google_assistant/helpers.py
COPY homeassistant/components/google_assistant/smart_home.py /usr/src/homeassistant/homeassistant/components/google_assistant/smart_home.py
COPY homeassistant/components/google_assistant/trait.py /usr/src/homeassistant/homeassistant/components/google_assistant/trait.py
COPY manifest.json /usr/local/share/google-execute-test-manifest.json
RUN python3 - <<'PYVERIFY'
import hashlib
import json
from pathlib import Path
from homeassistant.const import __version__
assert __version__ == "2026.10.0", __version__
manifest = json.loads(Path("/usr/local/share/google-execute-test-manifest.json").read_text())
for module in manifest["modules"]:
    path = Path("/usr/src/homeassistant") / module["path"]
    assert hashlib.sha256(path.read_bytes()).hexdigest() == module["after_sha256"], path
import homeassistant.components.google_assistant.helpers as helpers
import homeassistant.components.google_assistant.smart_home as smart_home
assert helpers.STATE_CONFIRMATION_TIMEOUT == 2
assert smart_home.EXECUTE_LIMIT == 2
PYVERIFY
RUN python3 -m compileall -q -f /usr/src/homeassistant/homeassistant/components/google_assistant/helpers.py /usr/src/homeassistant/homeassistant/components/google_assistant/smart_home.py /usr/src/homeassistant/homeassistant/components/google_assistant/trait.py
