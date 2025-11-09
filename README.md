

# Project Specification for Customized Chromium Build
## Objective
To create a customized version of the Chromium browser with specific features and optimizations tailored to our requirements



## Requirements
1. **Source Code Acquisition**: Clone the Chromium source code from the official repository.
2. **Development Environment**: Set up a C++ development environment with necessary tools and libraries
3. **Customization**: Only rebranding for now.
4. **Build Process**: Configure and execute the build process for Chromium.
5. **Testing**: Conduct thorough testing to ensure stability and performance of the customized build.
6. **Documentation**: Limited. Only document the customization and build process for future reference.
## Tools and Technologies
- C++ Programming Language
- Git for version control
- GN and Ninja build systems
- Visual Studio Code as the IDE
- Chromium's official build tools and dependencies
## Steps to Set Up the Workspace
1. **Clone the Repository**: Use Git to clone the Chromium source code.

```bash
git clone https://chromium.googlesource.com/chromium/src.git
```

2. **Install Dependencies**: Follow the official Chromium documentation to install all required dependencies for building Chromium on your operating system.
3. **Set Up Development Environment**: Configure Visual Studio Code with necessary extensions for C++
4. **Customize the Code**: Implement the desired customizations in the Chromium source code.
5. **Build the Project**: Use GN and Ninja to configure and build the customized Chromium

```bash
gn gen out/Default
ninja -C out/Default chrome
```

6. **Test the Build**: Run the built browser from the terminal.
