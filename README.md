# Zenchain Explorer Rust Services

Zenchain Explorer is a comprehensive block explorer and analytics platform tailored for the Zenchain blockchain. Originating as a fork from Blockscout, the Zenchain Explorer has undergone significant enhancements to improve functionality and ease of deployment across various operating systems.

The Zenchain Explorer ecosystem consists of the following components:

* Zenchain Explorer Backend <https://github.com/zenchain-protocol/zenchain-explorer-backend>
* Zenchain Explorer Frontend <https://github.com/zenchain-protocol/zenchain-explorer-frontend>
* Zenchain Explorer Rust Services (**the current repository**)

## Available Rust Services list

* Smart Contract Verifier ([smart-contract-verifier](smart-contract-verifier)): provides API for Ethereum contract verification written in Solidity and Vyper.
* Signatures Provider ([sig-provider](sig-provider)): aggregator of Ethereum signatures for transactions and events.
* EVM Visualizer ([visualizer](visualizer)): service for evm visualization such as Solidity contract visualization.
* Ethereum Bytecode Database ([eth-bytecode-db](eth-bytecode-db)): verifies smart contracts and searches for the sources via bytecodes.

# Development environment configuration

The process of setting up the development environment for Zenchain Explorer Rust Services, which is built using the Rust programming language, differs depending on the operating system in use. Rust's inherently multiplatform nature ensures that Zenchain Explorer Rust Services can be developed across various environments, including Linux, macOS, and Windows. This tutorial is designed to guide you through the preparation of your development environment, tailored to each of these operating systems.

## Dependencies

To successfully compile your code, it's essential to first install the required dependencies, with the installation process varying depending on your operating system.

### Git

Git is needed to get code from repositories.

#### Linux/WSL (Windows Subsystem for Linux)

Follow the instructions based on your Linux distribution (WSL by default installs Ubuntu) <https://git-scm.com/download/linux>

#### MacOS

Install Homebrew <https://brew.sh> and execute the following command:

```bash
brew install git
```

#### Windows

Download and execute the installer based on your architecture <https://git-scm.com/download/win>

### Rust

Download and install the SDK through `rustup` <https://www.rust-lang.org/tools/install>

#### Linux/WSL (Windows Subsystem for Linux)

`curl` package is needed, you can install it executing the following command (Ubuntu as reference):

```bash
sudo apt install -y curl
```

executing the following command:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

after installation restart the shell.

#### MacOS

Install `Xcode` from the App Store.

`curl` package is needed, you can install it executing the following command:

```bash
brew install curl
```

then install Rust with the following command:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

after installation restart the shell.

#### Windows

Download and execute the installer <https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-msvc/rustup-init.exe>

after installation restart the shell.

### Additional dependencies

#### Linux/WSL (Windows Subsystem for Linux)

Execute the following command (Ubuntu as reference):

```bash
sudo apt install -y clang libssl-dev llvm libudev-dev pkg-config make
```

##### Protocol Buffers v25.2

Execute the following commands (Ubuntu as reference):

```bash
wget https://github.com/protocolbuffers/protobuf/releases/download/v25.2/protoc-25.2-linux-x86_64.zip -O ./protoc.zip
unzip protoc.zip -d protoc
sudo mv ./protoc/include/* /usr/include
sudo mv ./protoc/bin/protoc /usr/bin/protoc
```

##### Protocol Buffers Gen OpenAPI v2.19.0

Execute the following commands (Ubuntu as reference):

```bash
wget https://github.com/grpc-ecosystem/grpc-gateway/releases/download/v2.19.0/protoc-gen-openapiv2-v2.19.0-linux-x86_64 -O ./protoc-gen-openapiv2
sudo mv ./protoc-gen-openapiv2 /usr/bin/protoc-gen-openapiv2
sudo chmod +x /usr/bin/protoc-gen-openapiv2
```

#### MacOS

If you have an Apple M1 ARM system, you must install `Apple Rosetta 2`:

```bash
softwareupdate --install-rosetta
```

Execute the following command to install additional deps:

```bash
brew install openssl
```

##### Protocol Buffers v25.2

TODO

##### Protocol Buffers Gen OpenAPI v2.19.0

TODO

#### Windows

##### LLVM

Download and execute the installer <https://github.com/llvm/llvm-project/releases/download/llvmorg-18.1.2/LLVM-18.1.2-win64.exe>

##### Protocol Buffers v25.2

<https://github.com/protocolbuffers/protobuf/releases/download/v25.2/protoc-25.2-win64.zip>

Once downloaded, extracts all files in a choosen path; then create the `PROTOC` environment variable that points to the protocol buffer executable, for example:

```bash
setx PROTOC C:\protoc\bin\protoc.exe /m
```

then restart the shell.

##### Protocol Buffers Gen OpenAPI v2.19.0

<https://github.com/grpc-ecosystem/grpc-gateway/releases/download/v2.19.0/protoc-gen-openapiv2-v2.19.0-windows-x86_64.exe>

Once downloaded, copy the file in a folder under `C:`, then add the folder path to the `PATH` environment variable.

## How to compile

Create a new folder, open it in the terminal and execute:

```bash
git clone https://github.com/zenchain-protocol/zenchain-explorer-rs
```

authenticate to GitHub, after confirmation, git starts cloning the repository.

Open the interested folder and execute the following commands:

```bash
cargo build --release
```

## Docker based development

You can also build and run each service within Docker directly.

### Without docker-compose

Open the service specific folder and then execute:

```bash
docker build -t zenchain-explorer/SERVICE_NAME .
```

then you can start the container with the following command:

```bash
docker run -dp localhost:PORT:PORT zenchain-explorer/SERVICE_NAME
```

### With docker-compose

Open the service specific folder and then execute:

```bash
docker compose up -d
```

starts a container using the `zenchain-explorer/SERVICE_NAME` built image and starts listening using the ports specified in the docker-compose.yml configuration file.
