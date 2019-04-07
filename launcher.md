# Launcher
They are used to start one daemon by business messaging desired.

It's the starting point of the application!

## Loading
The launcher are started with the [loader](../app/lib/launcher.js) script
during the main startup process.

They can be loaded from the global configuration file `config.json` or by
the individual configuration file `launcher.json`.

The first check is to know if the launcher is activate or not and
depending of the global, specific or default configuration the launcher
is started or not.

## Execution
During the first execution steps, we can see in the log or the console
the Controller loaded.

After the start the launcher are autonomous and don't need specific
attention.

## Organization
They are define in dedicated folder and they need at least the
following files:
- Module name
  - *run.js*: Scripts with the launcher code
  - *conf.json*: Default configuration file of the launcher

They are located in the './module' folder.

The JSON configuration file associate define the default configuration of the
launcher and its standard parameters plus the default behaviors.
This can be overloaded or completed by the global settings (`config.json`).
It also follow the folder structure and so the launcher chain/path and
its declaration.

## Editors' url to get doc & token
- Slack
  - https://guillain.slack.com/apps/manage/custom-integrations

- Google hangout chatbot
  - https://developers.google.com/hangouts/chat/how-tos/bots-publish
  - https://console.developers.google.com/apis/library/chat.googleapis.com

- Cisco Webex Teams
  - https://developer.webex.com/my-apps

- Cisco Jabber
  - https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/jabber/10_5/CJAB_BK_D6497E98_00_deployment-installation-guide-ciscojabber/configure_voice_and_video_communication.html

- Microsoft teams
  - https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.BotService%2FbotServices

## Example
### run.jss
```
// Load tools library
let Log = require(__basedir + 'lib/log');

// Load Botkit library
var Botkit = require(__basedir + 'botkit/lib/Botkit.js');

// Execute the main function
exports.run = function(config) {
  let controller = Botkit.web({
    debug: config.log.debug,
    studio_token: config.controller.on.botkit.token
  });

  let bot = controller.spawn({
    token: config.web.token
  }).startRTM();


  // Scenario declarations
  let scenario = require(__basedir + 'lib/controller.js');
  controller = scenario.run(controller);
  return controller;
};

```
### conf.json
```
{
    "launcher": {
        "MyLauncher": {
            "enable": true,
            "name": "corebot-framework",
            "msg": {
                "help": [
                    "MyLauncher help"
                ]
            }
        }
    }
}
```
