# Py3status Audio Module

This module provides a Py3status integration to manage and display audio information for the current audio output device. It uses `pactl` (PulseAudio Control) and `amixer` commands to interact with PulseAudio sinks and control audio settings.

## Features

- Displays the current audio output device, its volume, and mute status.
- Allows cycling through multiple audio output devices.
- Supports custom aliases for audio output device names.
- Handles mouse click events for:
  - Toggling mute/unmute.
  - Adjusting volume (increase/decrease).
  - Switching between audio output devices.

## Requirements

### Dependencies
- `pactl`: Command-line tool for interacting with PulseAudio.
- `amixer`: Command-line mixer for ALSA soundcard driver.

### Py3status
- This script is designed to be used as a Py3status module.

## Installation

1. Clone or download this repository.
2. Place the `audio.py` file in your Py3status configuration folder, typically located at `~/.config/i3status/py3status/`.
3. Add the module to your i3status configuration:
   ```plaintext
   order += "audio"
4. Optionally, configure the module parameters like this:
   ```plaintext
   audio {
       volume_step = 5
       output_aliases = "
           bluez_output.84_AC_60_29_EE_08.1:🎧,
           alsa_output.pci-0000_00_1f.3.analog-stereo:🔊
       "
   }
   ```

## Configuration

The following options can be configured in the Py3status module:

| Option           | Type    | Default Value | Description                                                                 |
|------------------|---------|---------------|-----------------------------------------------------------------------------|
| `output_aliases` | `str`   | `""`          | A string to define custom aliases for audio output devices.                |
| `muted_color`    | `str`   | `"#FF0000"`   | The color to display when the audio output is muted.                       |
| `volume_step`    | `int`   | `1`           | The percentage step to increase or decrease the volume.                    |
| `interval`       | `float` | `0.1`         | The refresh interval for the module, in seconds.                           |

### Example Configuration for `output_aliases`
You can provide aliases for audio outputs to display friendly names or icons. For example:
```python
output_aliases = "
    bluez_output.84_AC_60_29_EE_08.1:🎧,
    alsa_output.pci-0000_00_lf.3.analog-stereo:🔊
"
```

## Usage

### Displaying Audio Information
The `audio()` method fetches and formats the current audio output information, including volume percentage and mute status. It automatically applies aliases if provided.

### Mouse Click Controls
The `on_click(event)` method allows interaction with the audio outputs using mouse buttons:
- **Mute/Unmute**: Left-click on the module to toggle mute/unmute.
- **Change Output Device**: Right-click to cycle through available audio outputs.
- **Adjust Volume**: Scroll up to increase volume or scroll down to decrease volume.

## Example Output
When displayed in i3bar, the module might show:
<br>
<img src="example.gif"  height="260">

## Debugging

If you encounter issues with the module:
1. Ensure `pactl` and `amixer` are installed and accessible in your terminal.
2. Check that PulseAudio is running.
3. Test the commands manually in the terminal:
   ```bash
   pactl list sinks
   pactl info
   amixer -D pulse set Master mute
   ```

## License

This module is licensed under the MIT License.

## Contributions

Contributions are welcome! Feel free to open issues or submit pull requests.

