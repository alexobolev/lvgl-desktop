# Emscripten port

## Install Emscripten SDK

1. `git clone https://github.com/emscripten-core/emsdk.git <emsdk-path>`
1. `cd <emsdk-path>`
1. `git pull`
1. `./emsdk install latest`

Add the clone directory to PATH for further convenience.

---

## Build this project

1. `emsdk activate latest`
1. `<emsdk-path>/emsdk_env.bat`
1. `cd <lgvl-desktop-path>`
1. `mkdir cmbuild`
1. `cd cmbuild`
1. `emcmake cmake -G Ninja ..`
1. `cmake --build .`

A file `cmbuild/index.html` will be generated. You can open it in your browser.

---

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
