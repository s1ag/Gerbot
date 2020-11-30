# Table of Contents
1. [Goal](#goal)
2. [Installation](#installation)
3. [Usage](#usage)
4. [Contributing](#contributing)
5. [Creating a sample plugin](#creating-a-sample-plugin)
## Goal
Gerbot is a python-based Discord bot written for the University of Central Florida's IT Discord. It's goal is to provide UCF IT majors with opportunities to socialize, study, and gain opportunities through various channels dedicated to organizations/interests.


## Installation

To install Gerbot on your machine, go ahead and clone the respository by doing:

```bash
git clone https://github.com/s1ag/Gerbot
```

Then go ahead and create a virtual environment with venv like so:

```bash
python3 -m venv env
```
Once the virtual environment has been created, activate it:

Linux:
```bash
source env/bin/activate
```
Window's 10:
```bash
.\env\Scripts\activate
```
Upon being activated you should see `(env)` besides your terminal. Now install the dependencies:

```bash
pip3 install -r requirements.txt 
```

## Usage
To use Gerbot, you must supply a valid bot token. First create a file in the `src directory` called `.env`. Inside this file populate it as follows: 

```bash
BOT_TOKEN=DISCORD_TOKEN_HERE
```
Finally, run main.py and you should see that your bot is now running :)

```bash
python3 main.py
```
While development should be done using the venv, persistent deployment can be accomplished by using the Dockerfile provided in the repo. 

## Contributing
You will need to first fork the repo, then submit a pull request that will be reviewed by the development team. 

For suggestions/concerns please submit an issues ticket. Feel free to join us and become part of the development community through here: https://discord.gg/YM5QRzx 
 

## Creating a sample plugin

The plugins live within the cog directory, while the helper functions live outside the cog directory.

The code begins with imports 
```py
import discord 
from discord.ext import commands
```
Proceeded by a class based structure
```py
class Plugin(commands.Cog):
```

Create a init function within the class
```py
def __init__(self, bot):
  self.bot = bot
  self._last_member = None
 ```
 
 Use @commands.command to signify that it's a command, and assign it a list of aliases to use for others to reference upon:
 ```py
 @commands.command(aliases = ['example', 'test', 'sample'])
 ```
 Create a function, naming it anything. In this case, we'll call it first_plugin
 ```py
 async def simple_plugin(self, context, arg):
 ```
 Context is how we will send messages and access everything involving message data, async is referencing to async programming and is needed for discord.py to work. Arg is what will be passed in after our command. In this case it will be ping.
 
```py
if(arg == "ping"):
  await context.send("pong!")
```
We check to see if the argument passed is ping, and respond accordingly. 
To make sure that this plugin is loaded, we have to create a setup point like so:
```py 
def setup(bot):
    bot.add_cog(FirstPlugin(bot))
```
Full code:
```py
import discord
from discord.ext import commands
from system_utils.container_logger import container_logger
class FirstPlugin(commands.Cog):
    def __init__(self, bot):
        self.bot = bot
        self._last_member = None

    @commands.command(aliases = ['example', 'test', 'sample'])
    async def first_plugin(self, context):
        if(arg == "ping"):
            await context.send("pong")
        
def setup(bot):
    bot.add_cog(FirstPlugin(bot))
```

Congrulations! You've made your first plugin and dipped your toes into working with Gerbot.
