# Emscripten port

## Install Emscripten SDK

1. `git clone https://github.com/emscripten-core/emsdk.git <emsdk-path>`
1. `cd <emsdk-path>`
1. `git pull`
1. `./emsdk install latest`
1. To make CMake Presets work, add the cloned directory to `KURAGA_EMSDK_PATH` variable. Make sure it is not added to the admin account, unless of course you are building from under admin.

Add the clone directory to PATH for further convenience.


## Build this project

1. `emsdk activate latest`
1. `<emsdk-path>/emsdk_env.bat`
1. `cd <lgvl-desktop-path>`
1. `mkdir cmbuild`
1. `cd cmbuild`
1. `emcmake cmake -G Ninja ..`
1. `cmake --build .`

A file `cmbuild/index.html` will be generated. You can open it in your browser.


### Making this work with VS Code under Windows 10/11

* You'll need the basic C/C++ extensions: `C/C++` and `CMake Tools`, both by Microsoft.
* Open the folder in VS Code *at least once* from under a terminal where you have activated emscripten variables (see above).
* Configure `default` CMake preset using the CMake extension tab.
  * Be prepared to wait an eternity and a half until SDL2 checks all the symbols it wants.
  * The first build will take a while as it builds SDL2, LVGL and dependencies.
  * You can also just build things here, using `default` build preset.
* Once things have been configured, CMake's build tree contains absolute paths to all the emscripten tools you need, and VS Code should be able to pick things up from there.
* Now you can open the folder in VS Code however you want, and it should just work :tm:.

Do not use terminal to build the project while in VS Code.

### Build options (environment variables)

* `LVGL_CHOSEN_DEMO` can be set to the desired demo name so that you don't need to change any C files. This is useful to compile many demos in bulk using a script.

Example:
```bash
emcmake cmake .. -DLVGL_CHOSEN_DEMO=lv_demo_widgets
```

### Known issue with Google Chrome browser
Chrome might not be able to open the generated HTML file offline. It works if you copy the files to a server. Use Firefox or other browser for offline testing if needed.

### Known issue with Firefox
Firefox might not be able to open the generated HTML file offline unless you go to `about:config` and change `privacy.file_unique_origin` to `false`.
