# Columns UI

[![Build status](https://github.com/reupen/columns_ui/actions/workflows/build.yml/badge.svg)](https://github.com/reupen/columns_ui/actions/workflows/build.yml?query=branch%3Amaster)

Columns UI is released under the Lesser GNU Public Licence (see COPYING and COPYING.LESSER).

## Downloads

### Releases

Stable and pre-release versions can be downloaded from the [Columns UI home page](http://yuo.be/columns-ui).

### Development versions

The latest development version can be downloaded by clicking on the GitHub Actions badge above, and then 
clicking on the last successful build and scrolling down to the link named 'Component package (Release)'
at the bottom.

Development versions may be buggier than formal releases; if you encounter a problem, please open an issue.

## Development

To clone the repo and dependencies, [download and install Git](https://git-scm.com/downloads), and then run:

```powershell
git clone --recursive https://github.com/reupen/columns_ui.git
```

This repo makes use of Git submodules. If you're not familiar with them, [check out the guide here](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

### Build instructions

Visual Studio 2022 and the Windows 11 SDK are required to build Columns UI.

You can use the [free community edition of Visual Studio](https://www.visualstudio.com/downloads/).
During installation, select the Desktop development with C++ workload and the Windows 11 SDK from the right-hand side.

#### Installing vcpkg

Some dependencies are managed using [vcpkg](https://github.com/Microsoft/vcpkg) and it must be installed to build Columns UI.

You can install and set up vcpkg by running the following commands (in a directory of your choice outside the Columns UI source tree):

```powershell
git clone https://github.com/Microsoft/vcpkg.git
vcpkg\bootstrap-vcpkg.bat
vcpkg\vcpkg integrate install
```

Dependencies should then be automatically installed when Columns UI is built.

(You’ll need to occasionally run `git pull` in the vcpkg directory to fetch updated package metatdata.)

#### Building using the Visual Studio IDE

Open `vc17/columns_ui-public.sln` in Visual Studio 2022.

Select the Release configuration and the Win32 platform, and build the solution.

If the build is successful, `foo_ui_columns.dll` will be output in `vc17\Release`.

#### Building using MSBuild on the command line

You can use MSBuild if you prefer. In a Developer Command Prompt for VS 2022 (in the start menu), run:

```powershell
msbuild /m "/p:Platform=Win32;Configuration=Release" vc17\columns_ui-public.sln
```

If the build is successful, `foo_ui_columns.dll` will be output in `vc17\Release`.

For a clean build, run:

```powershell
msbuild /m "/p:Platform=Win32;Configuration=Release" "/t:Rebuild" vc17\columns_ui-public.sln
```

#### Using the Clang compiler (experimental)

Note: Currently not functional out of the box – should be functional again when the LLVM bundled with Visual Studio is updated to version 13.

Columns UI can be also compiled using the version of Clang distributed with Visual Studio. 

(Note that Clang is not installed by default – in the Visual Studio 2022 installer, you will need to select the Clang compiler and the Clang build tools components.)

With these installed, open a Developer Command Prompt for VS 2022 from the start menu, switch to the Columns UI source directory and run:

```powershell
msbuild /m "/p:PlatformToolset=ClangCL;UseLldLink=True;VcpkgAutoLink=False;WholeProgramOptimization=False;Platform=Win32;Configuration=Release" "/t:Rebuild" vc17\columns_ui-public.sln
```
