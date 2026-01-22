---
sidebar_position: 2
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Installing Agents

This page walks you through installing the OS dependencies and agent plugins needed for the demo.

## Stop Solace Agent Mesh

If Solace Agent Mesh is currently running, stop it by pressing **Ctrl+C** in the terminal (you may need to press it multiple times).

## Install OS Dependencies

The demo agents require **ImageMagick** and **ffmpeg** to be installed on your system.

<Tabs groupId="operating-system">
  <TabItem value="wsl" label="Windows WSL (Ubuntu)" default>

### ImageMagick

```bash
sudo apt update
sudo apt install imagemagick -y
magick --version
```

### ffmpeg

```bash
sudo apt install ffmpeg -y
ffmpeg -version
```

  </TabItem>
  <TabItem value="mac" label="macOS (Apple Silicon)">

### ImageMagick

```bash
brew install imagemagick
magick --version
```

:::note
Homebrew installs binaries to `/opt/homebrew/bin/`. If the command isn't found, ensure your shell profile (`.zshrc`) includes the Homebrew path.
:::

### ffmpeg

```bash
brew install ffmpeg
ffmpeg -version
```

  </TabItem>
</Tabs>

## Install Agent Plugins

Run the following script to install all required agent plugins:

```bash
#!/bin/bash
plugin_list=("web-agent" "artifact-host-agent" "imagemagick" "object-detection" "finance")
for plugin in "${plugin_list[@]}"; do
    sam plugin install git+https://github.com/gregmeldrum/solace-agent-mesh-plugins#subdirectory=${plugin}
    sam plugin add ${plugin} --plugin ${plugin}
done
```

You can save this as a script file and run it, or execute the commands manually for each plugin.

## Restart Solace Agent Mesh

Now that the agents are installed, restart Solace Agent Mesh:

```bash
sam run
```

## Verify Agents

After startup, navigate to [http://localhost:8000](http://localhost:8000) and click the **Agents** tab on the left sidebar. You should see several agents available including:

- **Web Agent** - Pulls information from the web and performs web searches
- **Artifact Host Agent** - Hosts HTML and images created by the system on a web server
- **ImageMagick Agent** - Resizes, crops images and adds text overlays
- **Object Detection Agent** - Uses a YOLO model to detect objects in images
- **Finance Agent** - Provides financial data and analysis

## Next Steps

Proceed to [Running the Demo](./running-demo) to try out the agents with sample prompts.
