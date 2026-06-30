
How to Use After Running the Commands Abovebash

Check everything
~/openwebui-manager/health-all.sh

Start all six servers at once
~/openwebui-manager/start-all.sh

Stop all six servers at once
~/openwebui-manager/stop-all.sh

Individual Control (still available)Old servers: ~/testwebui/start.sh, ~/openwebui2ver7/start.sh, ~/openwebui3/start.sh New servers: ~/testwebui-v10/start.sh, ~/openwebui2ver7-v10/start.sh, ~/openwebui4/start.sh

# -Open-WebUI-Additional-Three-Installer-v10.5
How to use itPaste the big block above into your terminal and press Enter. Review the created file if you want:bash  cat ~/install-openwebui-v10.5-new.sh | head -100  Run the installer:bash  ~/install-openwebui-v10.5-new.sh  After it finishes, you can start the new stack with:bash  ~/openwebui-manager/start-all.sh ~/openwebui-manager/health-all.sh


✅ openwebui2ver7-v10 setup complete

🎉 Installation of additional v10.5 instances complete!

Useful commands (new v10.5 stack only):
   ~/openwebui-manager/start-all.sh     # Start the three new ones
   ~/openwebui-manager/stop-all.sh      # Stop the three new ones
   ~/openwebui-manager/health-all.sh    # Health check

Individual control:
   ~/testwebui-v10/start.sh
   ~/openwebui2ver7-v10/start.sh
   ~/openwebui4/start.sh

Your original three servers (testwebui, openwebui2ver7, openwebui3) are untouched.


How to use itPaste the big block above into your terminal and press Enter.
Review the created file if you want:bash

cat ~/install-openwebui-v10.5-new.sh | head -100

Run the installer:bash

~/install-openwebui-v10.5-new.sh

After it finishes, you can start the new stack with:bash

 Here's exactly how to safely map your home folder before adding the three new Open WebUI servers.Step 1: Run this inspection command firstCopy and paste the entire block below into your terminal:bash

echo "=================================================="
echo "📁 MAPPING YOUR HOME DIRECTORY (~)"
echo "=================================================="
echo ""
echo "=== All top-level items in ~ (sorted) ==="
ls -1 ~ | sort

echo ""
echo "=== Only directories in ~ ==="
ls -d ~/*/ 2>/dev/null | sort

echo ""
echo "=================================================="
echo "🔍 CHECKING FOR CONFLICTS WITH THE NEW INSTALLER"
echo "=================================================="
echo ""

for name in openwebui-manager testwebui openwebui2ver7 openwebui3; do
    if [ -e ~/"$name" ]; then
        echo "⚠️  EXISTS: ~/$name"
        ls -ld ~/"$name"
        if [ -d ~/"$name" ]; then
            echo "   → Top-level contents:"
            ls -1 ~/"$name" | head -15
            echo ""
        fi
    else
        echo "✅ FREE: ~/$name (no conflict)"
    fi
done

echo ""
echo "=================================================="
echo "🧠 Checking existing Ollama & Open WebUI processes"
echo "=================================================="
echo ""
echo "Ollama installed?"
which ollama && ollama --version || echo "Ollama not found in PATH"

echo ""
echo "Running processes (open-webui / ollama):"
ps aux | grep -E 'open-webui|ollama' | grep -v grep || echo "No matching processes found"

echo ""
echo "Listening ports (11434 = Ollama, others = possible WebUIs):"
ss -tlnp | grep -E '11434|8080|8000|8001|3000' || echo "No relevant ports listening"

What this tells youFolder the new script creates
What happens if it already exists
Risk Level
~/openwebui-manager
Script will rename it to .backup.YYYYMMDD_HHMMSS
Low
~/testwebui
Same — automatic backup
Low
~/openwebui2ver7
Same — automatic backup
Low
~/openwebui3
Same — automatic backup
Low

The script is actually quite safe because it has this backup logic built in.Step 2: What you should do nextRun the inspection command above and paste the output here if you want me to analyze it for you.
Look especially for any existing folders that might be your current three servers (they probably have different names than testwebui, openwebui2ver7, openwebui3).
Check disk space:

bash

df -h ~
du -sh ~/* 2>/dev/null | sort -hr | head -20

Quick Summary of What the New Script Will CreateThe installer (install-openwebui-v10.5.sh) will create:~/openwebui-manager/ → management scripts (start-all.sh, stop-all.sh, health-all.sh)
Three new independent instances:~/testwebui/ (port 8080)
~/openwebui2ver7/ (port 8000)
~/openwebui3/ (port 8001)

Each instance gets its own:data/, models/, logs/, run/, Python venv, .env, secret key, start.sh/stop.sh

They will share one Ollama instance (on port 11434).Would you like me to:A. Give you a modified version of the installer that uses different/safer folder names (recommended if you already have folders with similar names)?B. Help you interpret the output after you run the inspection command?C. Show you how to manually back up your current three servers before running the new installer?Just reply with the output of the inspection command (or say A/B/C) and I’ll guide you precisely.

Explore Open WebUI environment variables

Learn about Linux systemd services

Add disk space check to script

devoshireroad777@DESKTOP-G3R5JB2:~$ echo "=================================================="
echo " MAPPING YOUR HOME DIRECTORY (~)"
echo "=================================================="
echo ""
echo "=== All top-level items in ~ (sorted) ==="
ls -1 ~ | sortecho ""
echo "=== Only directories in ~ ==="
ls -d ~/*/ 2>/dev/null | sortecho ""
echo "=================================================="
echo " CHECKING FOR CONFLICTS WITH THE NEW INSTALLER"
echo "=================================================="
echo ""for name in openwebui-manager testwebui openwebui2ver7 openwebui3; do
    if [ -e ~/"$name" ]; then
        echo "  EXISTS: ~/$name"
        ls -ld ~/"$name"
        if [ -d ~/"$name" ]; then
            echo "   → Top-level contents:"
            ls -1 ~/"$name" | head -15
            echo ""
        fi
    else
        echo " FREE: ~/$name (no conflict)"
    fi
doneecho ""
echo "=================================================="
ss -tlnp | grep -E '11434|8080|8000|8001|3000' || echo "No relevant ports listening"ound"
==================================================
 MAPPING YOUR HOME DIRECTORY (~)
==================================================

=== All top-level items in ~ (sorted) ===
openwebui2ver7
openwebui2ver7.backup.20260612_015130
openwebui2ver7.backup.20260612_021501
openwebui3
rebuild_openwebui2ver7_v6.sh
rebuild_openwebui2ver7_v7.1a.sh
rebuild_openwebui2ver7_v7.2.sh
rebuild_openwebui2ver7_v7.3.sh
rebuild_openwebui2ver7_v7.4.sh
rebuild_openwebui3_v2.sh
rebuild_openwebui3_v4.sh
rotate-webui-key.sh
testwebui
weekly-security-check.sh=== Only directories in ~ ===
/home/devoshireroad777/openwebui2ver7.backup.20260612_015130/
/home/devoshireroad777/openwebui2ver7.backup.20260612_021501/
/home/devoshireroad777/openwebui2ver7/
/home/devoshireroad777/openwebui3/
/home/devoshireroad777/testwebui/==================================================
 CHECKING FOR CONFLICTS WITH THE NEW INSTALLER
==================================================

 FREE: ~/openwebui-manager (no conflict)
  EXISTS: ~/testwebui
drwxr-xr-x 3 devoshireroad777 devoshireroad777 4096 May  9 18:42 /home/devoshireroad777/testwebui
   → Top-level contents:
WEBUI_SECRET_KEY
env1
start-secure-local.sh
start-secure.sh
start.sh  EXISTS: ~/openwebui2ver7
drwx------ 7 devoshireroad777 devoshireroad777 4096 Jun 12 02:18 /home/devoshireroad777/openwebui2ver7
   → Top-level contents:
check-security.sh
data
env1
logs
models
run
start.sh
stop.sh  EXISTS: ~/openwebui3
drwx------ 7 devoshireroad777 devoshireroad777 4096 Jun 10 02:43 /home/devoshireroad777/openwebui3
   → Top-level contents:
check-security.sh
data
env1
logs
models
run
security-check.sh
start.sh
stop.sh==================================================
 Checking existing Ollama & Open WebUI processes
==================================================

Ollama installed?
/usr/local/bin/ollama
ollama version is 0.23.2Running processes (open-webui / ollama):
ollama       175  0.7  0.5 2411404 45740 ?       Ssl  22:50   0:04 /usr/local/bin/ollama serve
devoshi+     470  3.1 13.0 7209632 1051452 pts/0 Sl+  22:50   0:20 /home/devoshireroad777/testwebui/env1/bin/python3.12 /home/devoshireroad777/testwebui/env1/bin/open-webui serve --host 127.0.0.1 --port 8080
devoshi+     592  3.3 14.2 6330972 1146880 pts/2 Sl+  22:51   0:20 /home/devoshireroad777/openwebui2ver7/env1/bin/python /home/devoshireroad777/openwebui2ver7/env1/bin/open-webui serve --host 127.0.0.1 --port 8000
devoshi+     599  0.0  0.4 2197620 40108 pts/2   Sl+  22:51   0:00 ollama serve
devoshi+     664  3.3 14.2 6332284 1146396 pts/3 Sl+  22:51   0:19 /home/devoshireroad777/openwebui3/env1/bin/python /home/devoshireroad777/openwebui3/env1/bin/open-webui serve --host 127.0.0.1 --port 8001
devoshi+     676  0.2  0.5 2337864 45308 pts/3   Sl+  22:51   0:01 ollama serveListening ports (11434 = Ollama, others = possible WebUIs):
LISTEN 0      2048        127.0.0.1:8000       0.0.0.0:*    users:(("open-webui",pid=592,fd=27))
LISTEN 0      2048        127.0.0.1:8001       0.0.0.0:*    users:(("open-webui",pid=664,fd=27))
LISTEN 0      2048        127.0.0.1:8080       0.0.0.0:*    users:(("open-webui",pid=470,fd=27))
LISTEN 0      4096        127.0.0.1:11434      0.0.0.0:*
devoshireroad777@DESKTOP-G3R5JB2:~$

Great, thanks for running the inspection! Here's the clear picture:Current State of Your Home FolderYou already have exactly the three instances the new script targets:~/testwebui → running on 8080
~/openwebui2ver7 → running on 8000
~/openwebui3 → running on 8001

All three are active (using their own env1 Python environments, mostly Python 3.12).
Ollama (v0.23.2) is running and shared.
You also have several old backups and rebuild scripts.Important: The install-openwebui-v10.5.sh script will automatically back up your current testwebui, openwebui2ver7, and openwebui3 folders (renaming them with .backup.timestamp), then replace them with the new v10.5 versions.
It will also create the new ~/openwebui-manager.RecommendationSince you said you want to add three more servers (not replace the existing ones), do not run the installer as-is. It would replace what you have now.Instead, let's create a modified version that adds three new independent instances with different names/ports so nothing gets touched.Step-by-step: Add 3 New Servers SafelyCreate a new installer script with safe names:

bash

cat > ~/install-openwebui-v10.5-new.sh << 'V10.5NEW'
#!/usr/bin/env bash
set -euo pipefail
umask 077

echo "=================================================="
echo "🚀 Open WebUI Additional-Three Installer v10.5"
echo "=================================================="

MANAGER="$HOME/openwebui-manager"
mkdir -p "$MANAGER"/{backups,logs,run}

OLLAMA_PORT=11434

# === NEW INSTANCE NAMES & PORTS (no conflicts) ===
declare -A INSTANCES=(
  [testwebui-v10]=8082
  [openwebui2ver7-v10]=8002
  [openwebui4]=8003
)

# (Rest of the script is identical to your original — system deps, manager scripts, etc.)

# ===================== System deps =====================
echo "📦 Installing system dependencies..."
sudo apt update -y
sudo apt install -y curl ca-certificates gnupg lsb-release psmisc iproute2 zstd \
                    ffmpeg build-essential pkg-config software-properties-common

# Python 3.11 (for consistency with v10.5)
sudo add-apt-repository ppa:deadsnakes/ppa -y
sudo apt update -y
sudo apt install -y python3.11 python3.11-dev python3.11-venv python3.11-full python3-pip

if ! command -v ollama >/dev/null 2>&1; then
    echo "🧠 Installing Ollama..."
    curl -fsSL https://ollama.com/install.sh | sh
fi

# ===================== Management scripts (updated for new instances) =====================
cat > "$MANAGER/start-all.sh" << 'STARTALL'
#!/usr/bin/env bash
set -euo pipefail
echo "🚀 Starting Open WebUI v10.5 additional stack..."

if ! curl -fsS "http://127.0.0.1:11434/api/version" >/dev/null 2>&1; then
    echo "🔄 Starting shared Ollama..."
    nohup ollama serve > "$HOME/openwebui-manager/logs/ollama.log" 2>&1 &
    echo $! > "$HOME/openwebui-manager/run/ollama.pid"
    sleep 8
fi

for NAME in testwebui-v10 openwebui2ver7-v10 openwebui4; do
    if [ -x "$HOME/$NAME/start.sh" ]; then
        echo "Starting $NAME..."
        "$HOME/$NAME/start.sh"
        sleep 6
    fi
done
echo "✅ Additional stack started."
STARTALL
chmod +x "$MANAGER/start-all.sh"

# (stop-all.sh and health-all.sh similarly updated — I can expand if needed)

# ===================== Create the new instances =====================
for NAME in "${!INSTANCES[@]}"; do
    PORT=${INSTANCES[$NAME]}
    BASE="$HOME/$NAME"
    echo ""
    echo "🔄 Setting up $NAME (port $PORT)..."

    if [ -d "$BASE" ]; then
        echo "   Backing up old folder..."
        mv "$BASE" "$BASE.backup.$(date +%Y%m%d_%H%M%S)"
    fi

    mkdir -p "$BASE"/{data,models,logs,run}
    chmod 700 "$BASE" "$BASE"/{data,models,logs,run}

    python3.11 -m venv "$BASE/env"
    "$BASE/env/bin/pip" install --upgrade pip setuptools wheel
    "$BASE/env/bin/pip" install open-webui

    SECRET=$(python3.11 -c 'import secrets; print(secrets.token_urlsafe(48))')
    echo -n "$SECRET" > "$BASE/.webui_secret_key"
    chmod 600 "$BASE/.webui_secret_key"

    cat > "$BASE/.env" << ENV
WEBUI_PORT=$PORT
WEBUI_SECRET_KEY=$SECRET
WEBUI_AUTH=True
ENABLE_SIGNUP=False
OLLAMA_BASE_URL=http://127.0.0.1:$OLLAMA_PORT
HOST=127.0.0.1
PORT=$PORT
ENABLE_OTEL=false
ENV
    chmod 600 "$BASE/.env"

    cat > "$BASE/start.sh" << 'START'
#!/usr/bin/env bash
set -euo pipefail
BASE="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
cd "$BASE"
umask 077

[ -f .env ] && { set -a; . .env; set +a; }
export WEBUI_SECRET_KEY="$(cat .webui_secret_key 2>/dev/null || echo '')"

mkdir -p data models logs run
source env/bin/activate

NAME="$(basename "$BASE")"
echo "🚀 Starting $NAME → http://127.0.0.1:$WEBUI_PORT"
nohup open-webui serve --host 127.0.0.1 --port "$WEBUI_PORT" > logs/openwebui.log 2>&1 &
echo $! > run/openwebui.pid
echo "✅ $NAME started (PID $(cat run/openwebui.pid))"
START
    chmod +x "$BASE/start.sh"

    cat > "$BASE/stop.sh" << 'STOP'
#!/usr/bin/env bash
BASE="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
[ -f "$BASE/run/openwebui.pid" ] && kill "$(cat "$BASE/run/openwebui.pid")" 2>/dev/null || true
rm -f "$BASE/run/openwebui.pid"
echo "🛑 $(basename "$BASE") stopped."
STOP
    chmod +x "$BASE/stop.sh"

    echo "✅ $NAME setup complete"
done

echo ""
echo "🎉 Additional v10.5 instances installed!"
echo "Useful commands:"
echo "   ~/openwebui-manager/start-all.sh"
echo "   ~/openwebui-manager/stop-all.sh"
echo "   ~/openwebui-manager/health-all.sh"
V10.5NEW

chmod +x ~/install-openwebui-v10.5-new.sh
echo "✅ New safe installer created: ~/install-openwebui-v10.5-new.sh"

Review and run it:

bash

cat ~/install-openwebui-v10.5-new.sh   # check it
~/install-openwebui-v10.5-new.sh

This will add:testwebui-v10 (8082)
openwebui2ver7-v10 (8002)
openwebui4 (8003)

Completely separate from your current servers.Would you like me to:Expand the full modified script with complete stop-all.sh + health-all.sh?
Or adjust the names/ports?
Or give you commands to stop/start everything cleanly?

Just say the word and paste any output if something unexpected happens.

Explore Ollama model management

Learn about systemd service units

Expand stop and health scripts

Please continue with your idea to Expand the full modified script with complete stop-all.sh + health-all.sh.

 Here is the complete, ready-to-use modified installer with fully expanded start-all.sh, stop-all.sh, and health-all.sh scripts tailored to your new safe instance names.New instances created:~/testwebui-v10 → port 8082
~/openwebui2ver7-v10 → port 8002
~/openwebui4 → port 8003

These will not touch your existing running servers.Full Installer ScriptCopy and paste the entire block below into your terminal:bash

cat > ~/install-openwebui-v10.5-new.sh << 'V10.5NEW'
#!/usr/bin/env bash
set -euo pipefail
umask 077

echo "=================================================="
echo "🚀 Open WebUI Additional-Three Installer v10.5"
echo "   Safe Add-On Mode • Does NOT touch existing servers"
echo "=================================================="

MANAGER="$HOME/openwebui-manager"
mkdir -p "$MANAGER"/{backups,logs,run}

OLLAMA_PORT=11434

# ===================== NEW SAFE INSTANCE NAMES & PORTS =====================
declare -A INSTANCES=(
  [testwebui-v10]=8082
  [openwebui2ver7-v10]=8002
  [openwebui4]=8003
)

# ===================== System deps =====================
echo "📦 Installing system dependencies..."
sudo apt update -y
sudo apt install -y curl ca-certificates gnupg lsb-release psmisc iproute2 zstd \
                    ffmpeg build-essential pkg-config software-properties-common

# Python 3.11
sudo add-apt-repository ppa:deadsnakes/ppa -y
sudo apt update -y
sudo apt install -y python3.11 python3.11-dev python3.11-venv python3.11-full python3-pip

if ! command -v ollama >/dev/null 2>&1; then
    echo "🧠 Installing Ollama..."
    curl -fsSL https://ollama.com/install.sh | sh
fi

# ===================== Management scripts =====================

# --- start-all.sh (for the new v10.5 instances only) ---
cat > "$MANAGER/start-all.sh" << 'STARTALL'
#!/usr/bin/env bash
set -euo pipefail
echo "🚀 Starting Open WebUI v10.5 Additional Stack..."

if ! curl -fsS "http://127.0.0.1:11434/api/version" >/dev/null 2>&1; then
    echo "🔄 Starting shared Ollama..."
    nohup ollama serve > "$HOME/openwebui-manager/logs/ollama.log" 2>&1 &
    echo $! > "$HOME/openwebui-manager/run/ollama.pid"
    sleep 8
fi

for NAME in testwebui-v10 openwebui2ver7-v10 openwebui4; do
    if [ -x "$HOME/$NAME/start.sh" ]; then
        echo "Starting $NAME..."
        "$HOME/$NAME/start.sh"
        sleep 6
    fi
done
echo "✅ Additional v10.5 stack started."
STARTALL
chmod +x "$MANAGER/start-all.sh"

# --- stop-all.sh (for the new v10.5 instances only) ---
cat > "$MANAGER/stop-all.sh" << 'STOPALL'
#!/usr/bin/env bash
set -euo pipefail
echo "🛑 Stopping Open WebUI v10.5 Additional Stack..."

for dir in ~/testwebui-v10 ~/openwebui2ver7-v10 ~/openwebui4; do
    if [ -f "$dir/run/openwebui.pid" ]; then
        PID=$(cat "$dir/run/openwebui.pid")
        if kill -0 "$PID" 2>/dev/null; then
            kill "$PID" 2>/dev/null || true
            echo "Stopped $dir (PID $PID)"
        fi
        rm -f "$dir/run/openwebui.pid"
    fi
done

if [ -f "$HOME/openwebui-manager/run/ollama.pid" ]; then
    PID=$(cat "$HOME/openwebui-manager/run/ollama.pid")
    if kill -0 "$PID" 2>/dev/null; then
        kill "$PID" 2>/dev/null || true
        echo "Stopped managed Ollama (PID $PID)"
    fi
    rm -f "$HOME/openwebui-manager/run/ollama.pid"
fi

echo "✅ Additional v10.5 stack stopped."
STOPALL
chmod +x "$MANAGER/stop-all.sh"

# --- health-all.sh (for the new v10.5 instances only) ---
cat > "$MANAGER/health-all.sh" << 'HEALTH'
#!/usr/bin/env bash
set -euo pipefail
echo "🔐 Open WebUI v10.5 Additional Stack - Health Report"
echo "=================================================="
echo "Date: $(date)"
echo ""

# Ollama
if curl -fsS "http://127.0.0.1:11434/api/version" >/dev/null 2>&1; then
    echo "Ollama (11434): ✅ OK"
else
    echo "Ollama (11434): ❌ DOWN"
fi
echo ""

for dir in ~/testwebui-v10 ~/openwebui2ver7-v10 ~/openwebui4; do
    [ -d "$dir" ] || continue
    NAME=$(basename "$dir")
    PORT=$(grep '^WEBUI_PORT=' "$dir/.env" 2>/dev/null | cut -d= -f2 || echo "??")
    CODE=$(curl -fsS -o /dev/null -w "%{http_code}" "http://127.0.0.1:$PORT" 2>/dev/null || echo "000")
    STATUS="⚠️ Not responding"
    if [[ "$CODE" =~ ^(200|302)$ ]]; then
        STATUS="✅ Running"
    fi
    echo "Instance: $NAME (port $PORT) → $STATUS"
    echo "   Disk: Data=$(du -sh "$dir/data" 2>/dev/null | cut -f1 || echo "N/A") | Models=$(du -sh "$dir/models" 2>/dev/null | cut -f1 || echo "N/A")"
    echo ""
done
HEALTH
chmod +x "$MANAGER/health-all.sh"

# ===================== Create the three new instances =====================
for NAME in "${!INSTANCES[@]}"; do
    PORT=${INSTANCES[$NAME]}
    BASE="$HOME/$NAME"
    echo ""
    echo "🔄 Setting up NEW instance: $NAME (port $PORT)..."

    if [ -d "$BASE" ]; then
        echo "   Existing folder found → backing up..."
        mv "$BASE" "$BASE.backup.$(date +%Y%m%d_%H%M%S)"
    fi

    mkdir -p "$BASE"/{data,models,logs,run}
    chmod 700 "$BASE" "$BASE"/{data,models,logs,run}

    python3.11 -m venv "$BASE/env"
    "$BASE/env/bin/pip" install --upgrade pip setuptools wheel
    "$BASE/env/bin/pip" install open-webui

    SECRET=$(python3.11 -c 'import secrets; print(secrets.token_urlsafe(48))')
    echo -n "$SECRET" > "$BASE/.webui_secret_key"
    chmod 600 "$BASE/.webui_secret_key"

    cat > "$BASE/.env" << ENV
WEBUI_PORT=$PORT
WEBUI_SECRET_KEY=$SECRET
WEBUI_AUTH=True
ENABLE_SIGNUP=False
OLLAMA_BASE_URL=http://127.0.0.1:$OLLAMA_PORT
HOST=127.0.0.1
PORT=$PORT
ENABLE_OTEL=false
ENV
    chmod 600 "$BASE/.env"

    # start.sh for this instance
    cat > "$BASE/start.sh" << 'START'
#!/usr/bin/env bash
set -euo pipefail
BASE="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
cd "$BASE"
umask 077

[ -f .env ] && { set -a; . .env; set +a; }
export WEBUI_SECRET_KEY="$(cat .webui_secret_key 2>/dev/null || echo '')"

mkdir -p data models logs run
source env/bin/activate

NAME="$(basename "$BASE")"
echo "🚀 Starting $NAME → http://127.0.0.1:$WEBUI_PORT"
nohup open-webui serve --host 127.0.0.1 --port "$WEBUI_PORT" > logs/openwebui.log 2>&1 &
echo $! > run/openwebui.pid
echo "✅ $NAME started (PID $(cat run/openwebui.pid))"
START
    chmod +x "$BASE/start.sh"

    # stop.sh for this instance
    cat > "$BASE/stop.sh" << 'STOP'
#!/usr/bin/env bash
BASE="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
if [ -f "$BASE/run/openwebui.pid" ]; then
    PID=$(cat "$BASE/run/openwebui.pid")
    if kill -0 "$PID" 2>/dev/null; then
        kill "$PID" 2>/dev/null || true
    fi
    rm -f "$BASE/run/openwebui.pid"
fi
echo "🛑 $(basename "$BASE") stopped."
STOP
    chmod +x "$BASE/stop.sh"

    echo "✅ $NAME setup complete"
done

echo ""
echo "🎉 Installation of additional v10.5 instances complete!"
echo ""
echo "Useful commands (new v10.5 stack only):"
echo "   ~/openwebui-manager/start-all.sh     # Start the three new ones"
echo "   ~/openwebui-manager/stop-all.sh      # Stop the three new ones"
echo "   ~/openwebui-manager/health-all.sh    # Health check"
echo ""
echo "Individual control:"
echo "   ~/testwebui-v10/start.sh"
echo "   ~/openwebui2ver7-v10/start.sh"
echo "   ~/openwebui4/start.sh"
echo ""
echo "Your original three servers (testwebui, openwebui2ver7, openwebui3) are untouched."
V10.5NEW

chmod +x ~/install-openwebui-v10.5-new.sh
echo ""
echo "✅ Full safe installer created: ~/install-openwebui-v10.5-new.sh"
echo "Run it with: ~/install-openwebui-v10.5-new.sh"

How to use itPaste the big block above into your terminal and press Enter.
Review the created file if you want:bash

cat ~/install-openwebui-v10.5-new.sh | head -100

Run the installer:bash

~/install-openwebui-v10.5-new.sh

After it finishes, you can start the new stack with:bash

~/openwebui-manager/start-all.sh
~/openwebui-manager/health-all.sh

Your original three servers will continue running normally on their current ports.Would you like me to also give you a combined start-all.sh / health-all.sh that manages both your old servers + the new ones? Or any other adjustments?

Configure systemd services for stability

Explore Ollama model quantization benefits

Yes this is a good idea please do this,  give you a combined start-all.sh / health-all.sh that manages both your old servers + the new ones

 Perfect! Here's the combined management scripts that control all six servers (your original three + the three new v10.5 ones) from one place.Combined Scripts (All Six Instances)Run these three commands to update your ~/openwebui-manager/ with the combined versions:bash

# 1. Combined start-all.sh (starts Ollama if needed + all 6 servers)
cat > ~/openwebui-manager/start-all.sh << 'STARTALL'
#!/usr/bin/env bash
set -euo pipefail
echo "🚀 Starting ALL Open WebUI Servers (Old + New v10.5)..."

# Start shared Ollama if not running
if ! curl -fsS "http://127.0.0.1:11434/api/version" >/dev/null 2>&1; then
    echo "🔄 Starting shared Ollama..."
    nohup ollama serve > "$HOME/openwebui-manager/logs/ollama.log" 2>&1 &
    echo $! > "$HOME/openwebui-manager/run/ollama.pid"
    sleep 8
fi

# All six instances
ALL_NAMES=(testwebui openwebui2ver7 openwebui3 testwebui-v10 openwebui2ver7-v10 openwebui4)

for NAME in "${ALL_NAMES[@]}"; do
    if [ -x "$HOME/$NAME/start.sh" ]; then
        echo "Starting $NAME..."
        "$HOME/$NAME/start.sh"
        sleep 5
    else
        echo "⚠️  $NAME not found or no start.sh"
    fi
done

echo "✅ ALL servers started."
echo ""
echo "Run: ~/openwebui-manager/health-all.sh   to check status"
STARTALL
chmod +x ~/openwebui-manager/start-all.sh

# 2. Combined stop-all.sh
cat > ~/openwebui-manager/stop-all.sh << 'STOPALL'
#!/usr/bin/env bash
set -euo pipefail
echo "🛑 Stopping ALL Open WebUI Servers (Old + New v10.5)..."

ALL_NAMES=(testwebui openwebui2ver7 openwebui3 testwebui-v10 openwebui2ver7-v10 openwebui4)

for NAME in "${ALL_NAMES[@]}"; do
    DIR="$HOME/$NAME"
    if [ -f "$DIR/run/openwebui.pid" ]; then
        PID=$(cat "$DIR/run/openwebui.pid" 2>/dev/null || echo "")
        if [ -n "$PID" ] && kill -0 "$PID" 2>/dev/null; then
            kill "$PID" 2>/dev/null || true
            echo "Stopped $NAME (PID $PID)"
        fi
        rm -f "$DIR/run/openwebui.pid"
    fi
done

# Stop managed Ollama (if we started it)
if [ -f "$HOME/openwebui-manager/run/ollama.pid" ]; then
    PID=$(cat "$HOME/openwebui-manager/run/ollama.pid" 2>/dev/null || echo "")
    if [ -n "$PID" ] && kill -0 "$PID" 2>/dev/null; then
        kill "$PID" 2>/dev/null || true
        echo "Stopped managed Ollama (PID $PID)"
    fi
    rm -f "$HOME/openwebui-manager/run/ollama.pid"
fi

echo "✅ ALL servers stopped."
STOPALL
chmod +x ~/openwebui-manager/stop-all.sh

# 3. Combined health-all.sh
cat > ~/openwebui-manager/health-all.sh << 'HEALTH'
#!/usr/bin/env bash
set -euo pipefail
echo "🔐 Open WebUI - FULL Health Report (All 6 Servers)"
echo "=================================================="
echo "Date: $(date)"
echo ""

# Ollama status
if curl -fsS "http://127.0.0.1:11434/api/version" >/dev/null 2>&1; then
    echo "Ollama (11434): ✅ OK"
else
    echo "Ollama (11434): ❌ DOWN"
fi
echo ""

ALL_NAMES=(testwebui openwebui2ver7 openwebui3 testwebui-v10 openwebui2ver7-v10 openwebui4)

for NAME in "${ALL_NAMES[@]}"; do
    DIR="$HOME/$NAME"
    [ -d "$DIR" ] || { echo "⚠️  $NAME: Folder not found"; echo ""; continue; }

    PORT=$(grep '^WEBUI_PORT=' "$DIR/.env" 2>/dev/null | cut -d= -f2 || echo "??")
    CODE=$(curl -fsS -o /dev/null -w "%{http_code}" "http://127.0.0.1:$PORT" 2>/dev/null || echo "000")

    if [[ "$CODE" =~ ^(200|302)$ ]]; then
        STATUS="✅ Running"
    else
        STATUS="⚠️ Not responding (HTTP $CODE)"
    fi

    DATA_SIZE=$(du -sh "$DIR/data" 2>/dev/null | cut -f1 || echo "N/A")
    MODELS_SIZE=$(du -sh "$DIR/models" 2>/dev/null | cut -f1 || echo "N/A")

    echo "Instance: $NAME (port $PORT) → $STATUS"
    echo "   Disk: Data=$DATA_SIZE | Models=$MODELS_SIZE"
    echo ""
done

echo "=================================================="
echo "Tip: Use ~/openwebui-manager/start-all.sh or stop-all.sh"
HEALTH
chmod +x ~/openwebui-manager/health-all.sh

echo ""
echo "✅ Combined management scripts updated successfully!"
echo ""
echo "Now you can use:"
echo "   ~/openwebui-manager/start-all.sh     # Start ALL 6 servers"
echo "   ~/openwebui-manager/stop-all.sh      # Stop ALL 6 servers"
echo "   ~/openwebui-manager/health-all.sh    # Full health report for all 6"

How to Use After Running the Commands Abovebash

# Check everything
~/openwebui-manager/health-all.sh

# Start all six servers at once
~/openwebui-manager/start-all.sh

# Stop all six servers at once
~/openwebui-manager/stop-all.sh

Individual Control (still available)Old servers: ~/testwebui/start.sh, ~/openwebui2ver7/start.sh, ~/openwebui3/start.sh
New servers: ~/testwebui-v10/start.sh, ~/openwebui2ver7-v10/start.sh, ~/openwebui4/start.sh

Would you like me to also create a single all-servers.sh wrapper or any other helper scripts (e.g., restart-all, backup-all, etc.)? Just let me know!





~/openwebui-manager/start-all.sh
~/openwebui-manager/health-all.sh

Your original three servers will continue running normally on their current ports.Would you like me to also give you a combined start-all.sh / health-all.sh that manages both your old servers + the new ones? Or any other adjustments?

