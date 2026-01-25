# Gemini Web CLI

[![asciicast](https://asciinema.org/a/UJgIuzvxHuZ4kux15yYWESKlG.svg)](https://asciinema.org/a/UJgIuzvxHuZ4kux15yYWESKlG)

A minimal command-line interface for interacting with Google Gemini AI using [the reverse-engineered web API](https://github.com/HanaokaYuzu/Gemini-API).

## Example Installation Guide

```sh
git clone https://github.com/hurryman2212/gemini-webcli.git
cd gemini-webcli
python -m venv .
source bin/activate
pip install -r requirements.txt
```

## Example Usage Guide

```sh
# cd gemini-webcli
# source bin/activate
./gemini-webcli -h
```

### Interactive Mode

Choose between two modes:
- **send_message()** - Start chat using Gemini 3.0 Pro model with conversation history.
- **generate_content()** - Single-shot image generation using Nano Banana Pro model (in loop). The temporal file `./temp.png` will be saved and a native Python window showing thg image will be opened. The file will be deleted after the window is closed.

### One-Shot Command Mode

Use command-line options for quick, non-interactive queries:

- **`-e COMMAND`** or **`--explain COMMAND`** - Get a brief explanation of a shell command.
  ```sh
  ./gemini-webcli -e "ls -la"
  ```

- **`-s DESCRIPTION`** or **`--suggest DESCRIPTION`** - Get a shell command suggestion based on your description.
  ```sh
  ./gemini-webcli -s "list all files including hidden ones"
  ```
The result from the above command is automatically copied to your clipboard.

- **`-n PROMPT SYSTEM_PROMPT`** - Optimized command to accept nyarchassistant JSON format prompt and system prompt.
 
Use the following command in nyarchassistant (Settings -> LLM -> Custom Command -> Command to execute to get bot output):
```
read -r -d '' RAW_PROMPT <<\EOF_PROMPT
{0}
EOF_PROMPT
read -r -d '' RAW_SYSTEM <<\EOF_SYSTEM
{1}
EOF_SYSTEM
__VENV_PATH__/python __VENV_PATH__/gemini-webcli -n "$RAW_PROMPT" "$RAW_SYSTEM"
```

(replace `__VENV_PATH__` with your actual path)

**Note:** All the above options are mutually exclusive with each other.

### Input

- Type your message like in a typical multi-line text editor.
- Then press **Ctrl+D** (End-of-file) to submit.
- Press **Ctrl+C** during the prompt to exit.

## `cookie.bin` File

This binary file is created to save session metadata (conversation history) in binary format. Automatically created and updated during chat sessions. Safe to delete to start fresh conversations.
