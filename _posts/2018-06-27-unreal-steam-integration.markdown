So I started with a steam / unreal integration. There where several issues which took quite a time to figure out. Due to the fact that documentation is pretty lacking I decided that I will publish a list which hopefully helps other devs in getting started and/or troubleshooting. 

Just be aware it is the first time for me working with the steam framework and the game I am working is not shipped yet so this list is not complete.

- Steam works out of the box in unreal. There is no need to setup. Just activate the plugin.
- When testing the steam integration you need to have steam running.
- Launching the game via PIE will not start the steam online subsystem. So PIE is a no go for testing.
- The Standalone version seems to be fragile when trying to connect / host a listen server sessions. Sometimes it works sometimes not. Use a packaged build or start it via the DebugGame / DevelopmentGame targets. This could be due to the test appid.
- When testing, both steam applications needs to be on the same download region.
- For proper steam integration tests you should use two seperate machines.
- The SteamDevAppId property in the DefaultEngine.ini is only for developme.nt builds
  - For shipping builds you need to put an steam_appid.txt file inside your win64 folder.


I hope this list will help fellow developers. 
Thanks, MadSystem
