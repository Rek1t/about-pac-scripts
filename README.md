# About PAC Scripts

## Setting PAC Script

### Windows 

On Windows you may set PAC script via `Win+R > inetcpl.cpl > Connections > LAN settings > Use automatic configuration script`

### Chromium

1. In Chromium settings there is a button for opening standard Linux/Windows dialog of setting PAC script.
2. Also Web Extensions of Chromium may set PAC script as a string and as URL via `chrome.proxy.settings`. This is implemented independently of the OS and has its own bugs.

### FireFox

`Browser > Options > Advanced > Network > Settings > Automatic proxy configuration URL`

## Caching of PAC Scripts

### Windows

Windows (winHttp, etc.) does very poor caching if any. Setting PAC script via URL in system settings results in server bombardment with requests.

### Chromium

If web extension set PAC script via URL then the script is loaded only once and cached. Cache overloading happens only on browser restarts. (checked on Chrome 55/Windows)

### Firefox

After setting PAC URL in browser settings it is loaded only once or twice and cached for a long period. (checked on Firefox 50/Windows)

## For Developers

1. PAC script is re-evaluated each time for each URL-resource loaded.
2. IE may be detected via [Conditional Compilation](http://stackoverflow.com/questions/10072816/how-does-this-ie-check-work) of comment content: `const isIE = /*@cc_on!@*/false;`

### Chromium Bugs

1. Web Extensions can't set PAC scripts larger than 1MB via URL, [bug](https://bugs.chromium.org/p/chromium/issues/detail?id=678022).
2. Web Extensions can't set scripts with non-ASCII chars as a string, unicode URLs must be punycoded.
3. Once I deleted all extensions from Chrome, but PAC script was still active and couldn't be purged via settings or browser restarts.

## Alerts and Debugging

1. Alert messages may be seen in Chromium network events: chrome://net-internals/#events
2. In Chromium you may check active proxy settings via chrome://net-internals/#proxy
