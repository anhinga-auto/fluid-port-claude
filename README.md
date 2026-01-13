# fluid-port-claude
ported the original anhinga/fluid project using Claude Code to JavaScript with shaders

 * note that this runs at 60 frames per second to match Processing `frameRate` default; but the actual rate in the Processing runs tends to be smaller (e.g. my laptop is currently running it at 24 frames per second)

 * you might want to further lower the rate; in this sense you might want to edit line 578 of the `web/index.html` file:
   
    * `this.frameCount = Math.floor(elapsed / (1000 / 60)); // virtual frames at 60fps`
