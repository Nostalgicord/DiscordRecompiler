# Discord Recompiler
A template for recompiling Discord (Windows only)

## Legal
This is for research purposes only, as such, this won't provide any Discord files for legality reasons, if you want to mod your Discord client, you're on your own, as always, no warranty!

## Contribute
Any steps needed to add can be appreciated.

## Things needed
- Asar (https://github.com/electron/asar)
- Yarn
- An editor of your choice
- Discord (you need the files as this won't provide you for legality reasons)

## Instructions
1. Download the project (via git clone or whatever)
2. If you're on yarn 2.0 and above, run `yarn config set nodeLinker node-modules`
3. Be sure to know the Electron version (for latest stable, latest Electron is your best bet, for others, google `How to check Elecron version`)
4. Go to `C:/Users/(your user)/Appdata/local/Discord/app-(version)/resources/`
5. Extract `app.asar` (asar extract app.asar app)
6. Move everything but node_modules from the app folder to the project directory
7. Move `bootstrap` folder (and `build_info.json` for latest versions) from the resource folder to the project directory.
8. Go to `C:/Users/(your user)/Appdata/local/Discord/app-(version)/` and copy `app.ico` to the project directory.
9. Go to `%appdata%/Discord/modules` (or `C:/Users/(your user)/Appdata/local/Discord/app-(version)/modules/` for some versions)
10. If you're in `C:/Users/(your user)/Appdata/local/Discord/app-(version)/modules`, then copy every folder to the project's modules directory, if not, then go to the individual folders, and copy to the modules folder in the the project's directory, be sure to remove the dummy file.
11. Open cmd in this folder and type `yarn install`, then `yarn add electron electron-builder electron-builder-squirrel-windows --dev`
12. Go to `package.json.example`, then copy the scripts block to your `package.json`, then in your `package.json`, modify the Electron version to your Discord's Electron version (be sure to not put a ^ in front of the version number), and insert author block and version block. Your `package.json` should look like `package.json.example`.
13. Go to `common/paths.js`, and add `exports.getExeDir = getExeDir;` below `exports.whatever = whatever;`, add `let (var) exeDir = null;` to `let (var) whatever = null;`, add `exeDir = _path.default.dirname(app.getPath('exe'));` under `require(electron)` line (if a similar line exists, remove it), change `moduleDataPath = _path.default.join(userDataVersionedPath, 'modules');` to `moduleDataPath = _path.default.join(exeDir, 'modules');` and add a function `getExeDir` with `return ExeDir` at the bottom of the file similar to the ones above.
14. Go to `common/moduleUpdater.js`, rename `paths.getUserDataVersioned()` to `paths.getExeDir()` and set `true` to variables `skipHostUpdate` and `skipModuleUpdate` to skip updating.
15. Extract `core.asar` from `modules/discord_desktop_core` and repeat steps 11 to 13 inside the extracted directory.
16. At `modules/discord_desktop_core`, run `asar pack core core.asar` (assuming the extracted folder is `core`, if not, change the first `core` to your extracted folder name)
17. Go back to the project root directory and run `yarn dist`
18. Install the installer from `dist/squirrel-windows-ia32` and you're done!