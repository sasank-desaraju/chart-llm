# Tinkering with LLMs

**Be advised:**
The config file in `.streamlit/config.toml` is setting this up to run on HPG and port forward to your local computer.
If you are running it locally, change the config (or just change its name so it doesn't get used).

## Requirements

*This is how I have it working on HPG; there may be other ways.*

Install Ollama and whatever chat models you want (at least llama3).

In conda env, install `python=3.10` and `streamlit`.
Install llama-index things using pip:
`pip install llama-index llama-index-core llama-index-llms-ollama`.

## Running on HPG

Use srun to request a GPU session.
I recommend making a handy script such as [this one](https://github.com/sasank-desaraju/med-ai-workflow/blob/main/interactive.sh).
Make sure to change your `account` and `qos` to the right ones.

Once using the interactive session (e.g. `./interactive.sh`), you should see your node name in the terminal (c1000a-s29 or so).
Open another terminal window on you local computer and start SSH port forwarding with `ssh -NL 8080:c1000a-s29:8080 albert.gator@hpg.rc.ufl.edu`, replacing the node name and user name with yours.
Now, open up a web browser and go to `http://localhost:8080`.

For running streamlit and ollama, I use `tmux` to get 2 terminal panes in the same session.
In one terminal window, start Ollama with `ollama serve`.
In the other, activate your conda env and run `streamlit run ollama-streamlit-app.py`.

You should see the app working in your browser window.

## Running locally

I haven't actually tried this but I assume it's like this:

Make sure the config in `.streamlit/config.toml` is disabled.

Open one terminal window and run `ollama serve` to start Ollama.

Open another terminal window, start your conda env, and run `streamlit run ollama-streamlit-app.py`.

The app should pop up in a browser window.
