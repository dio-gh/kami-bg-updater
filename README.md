# KAMI Background Updater

This is a Python script created for automatically updating [KAMI](https://github.com/isJuhn/KAMI) in the background, silently. It works by you manually adding it once to the Task Scheduler (on Windows), which will then periodically run it as per your configuration, and keep the emulator up-to-date for you without any interruption.

[KAMI](https://github.com/isJuhn/KAMI) could also inject a task roughly like this automatically, but it's pretty annoying to do that, and kind of ugly. It's also ever so slightly more secure this way.

## Requirements

This script depends on both 7-Zip and Python being installed, along with the `requests` Python library.

For installing 7-Zip on your system, see [here.](https://www.7-zip.org/download.html)

For installing Python on your system, see [here.](https://www.python.org/downloads/)

For installing the `requests` Python library, open the command line, and issue:

```
pip install requests
```

## Usage

### On Windows systems

<details>
<summary>Click here to expand...</summary>

1. Download the script from GitHub by
   * visiting the script file (`updater.py`) in the repository,
   * clicking on the `Raw` button to display the original file,
   * pressing `CTRL+S` to save it to your desired KAMI installation directory (where `KAMI.Windows.exe` is)

2. Open the Start Menu, then search for and open `Task Scheduler`

3. Click on `Create Task...`

4. Configure the updater task as follows:
   * for `Name`, give it something descriptive, like `KAMI Background Updater`
   * on the `Triggers` tab, add a new trigger:
     * for `Begin the task`, select `On Schedule`
     * for frequency, select `One time` (confusing, I know)
     * check the `Repeat task every:` checkbox, and set it to your liking (I use 15 mins)
     * at the `for a duration of:` drop-down, select `Indefinitely`
     * click `OK` to save it
   * on the `Actions` tab, add a new action:
     * for `Action:` you'll want `Start a program`
     * for `Program/script:` you'll want to simply type in `pythonw`
     * for `Add arguments:`, you'll need to provide the path to the script file
       * navigate to your KAMI installation directory where you've downloaded it
       * hold `CTRL` and right click
       * select `Copy full path`
       * paste it into the `Add arguments:` textbox (and don't remove the quotes around it)
     * click `OK` to save it
   * on the `Conditions` tab, check the `only if network connection is available` (optional)
   * click `OK` to finalize the task

If you've done everything correctly, the emulator will be kept up-to-date by this script, periodically polling for updates, and applying them as they come, seamlessly.
  
#### Troubleshooting

In case you find the script doesn't trigger as it should, you may want to force it to run as administrator. I'm not using Windows in English however, so I'd need to dig out the option names for that to put here, so just find them please yourself. I had this happen to me, so you'll probably need to do this too. Blame Microsoft.

</details>

### On Unix systems

The script won't work on Unix-like systems right now. Wouldn't take much to fix it, but I have no desire to. This way of manhandling the lifecycle management is a very Windows problem anyways.

## Notes and limitations

This script will only work as long as the build archive names match the current format, specifically till they contain the word `KAMI`.
