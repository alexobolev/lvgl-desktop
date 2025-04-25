# Emscripten port

## Common prerequisites

### Install Visual Studio 2022

* Full desktop installation will do: https://visualstudio.microsoft.com/vs/community/,
* or you may already have Build Tools installed.

Whichever installation you have, make sure that the common C++ development packages are available, including `C++ CMake tools for Windows`.

### Install Emscripten SDK

1. `git clone https://github.com/emscripten-core/emsdk.git <emsdk-path>`
1. `cd <emsdk-path>`
1. `git pull`
1. `./emsdk install latest`
1. To make CMake Presets work, add the cloned directory to `KURAGA_EMSDK_PATH` variable. Make sure it is not added to the admin account, unless of course you are building from under admin.

Add the clone directory to PATH for further convenience.


## Build this project

Clone this repository **with submodules**.

```
> git clone --recurse-submodules <repo-url>
```

Whether you're building from a terminal or Visual Studio, you will need to activate the emscripten environment:

```
> emsdk activate latest
> <emsdk-path>/emsdk_env.bat
```

### Use case: building using terminal only

```
cd <lgvl-desktop-path>
mkdir cmbuild
cd cmbuild
emcmake cmake -G Ninja ..
cmake --build .
```

### Use case: Visual Studio Code

Ensure you have the following prerequisites fulfilled:

* Visual Studio 2022 (or Build Tools) is installed.
  * This specifically requires `C++ CMake tools for Windows` package.
* Visual Studio Code is installed and available in `PATH`.
  * This should happen automatically if you have a system-wide installation.
  * If your Visual Studio Code is installed under `AppData`:
    * manually add the directory with `code.cmd` to `PATH`,
    * make sure to restart your terminal.
* Basic C/C++ extensions are installed: `C/C++` and `CMake Tools`, both by Microsoft. Throw in some debugger for good measure, too.

Once you have checked the prerequisites:

1. Open `Developer PowerShell for VS 2022` (it will provide `cmake`).
1. Activate emscripted using the two commands above.
1. Open the repository in VS Code *at least once* from under the terminal (`code .`).
1. Configure `default` CMake preset using the CMake extension tab.
   * Be prepared to wait an eternity and a half until SDL2 checks all the symbols it wants.
   * The first build will take a while as it builds SDL2, LVGL and dependencies.
   * You can also just build things here, using `default` build preset.
1. Once things have been configured, CMake's build tree contains absolute paths to all the emscripten tools you need, and VS Code should be able to pick things up from there.
   * Now you can open the folder in VS Code however you want, and it should just work :tm:.

Do not use terminal to build the project while in VS Code.

### Output

Whichever way you've chosen, a file `cmbuild/index.html` will be generated. You should be able to open it in your browser.

## Original notes from upstream

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
