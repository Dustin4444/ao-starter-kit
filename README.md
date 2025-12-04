# ao-starter-kit

> ⚠️ **Maintenance Notice**: This project is archived and no longer actively maintained. It is provided as-is for reference and educational purposes. While you are free to use, modify, and distribute this code under the MIT license, please be aware that:
> - No bug fixes or security updates will be provided
> - No new features will be added
> - Issues and pull requests will not be reviewed or merged
> - The code may contain outdated dependencies or practices
>
> If you find this project useful, feel free to fork it and maintain your own version.

A comprehensive boilerplate for setting up AO processes with testing, modules, and amalgamation alongside a React application. This starter kit simplifies the development and deployment of AO processes by providing pre-configured setups and example processes.

## Quick Start

The easiest way to get started is using the `create-ao-dapp` CLI tool:

```bash
npx create-ao-dapp@latest
```

This will scaffold a new AO dApp project with all the necessary boilerplate.

## What's Included

- **Backend Processes**: Pre-configured AO processes located in the `./ao` directory
- **Frontend Applications**: React-based frontend applications in the `./apps` directory
- **Build Scripts**: Automated build and deployment scripts
- **Testing Setup**: Busted testing framework configuration for Lua processes
- **Documentation**: Comprehensive documentation and examples

## Prerequisites

Before you begin, ensure you have the following installed:

- **Bun**: Fast JavaScript all-in-one toolkit ([Installation Guide](https://bun.sh/))
- **LuaRocks**: Package manager for Lua modules ([Installation Guide](https://luarocks.org/))
- **Busted**: Unit testing framework for Lua
- **Docker**: Containerization platform required for the build process ([Download Docker](https://www.docker.com/))

### Installing Prerequisites

1. **Bun**: Follow the installation instructions on the [Bun.sh website](https://bun.sh/)

2. **LuaRocks**: Follow the installation instructions on the [LuaRocks website](https://luarocks.org/)

3. **Busted**: Install via LuaRocks:
   ```bash
   luarocks install busted
   ```

4. **Docker**: Download and install Docker from the [official Docker website](https://www.docker.com/)

## Project Structure

```
ao-starter-kit/
├── ao/                    # Backend processes
│   └── [process-name]/    # Individual process directories
├── apps/                  # Frontend applications
│   └── [app-name]/        # Individual app directories
├── examples/              # Example projects
└── create-ao-dapp/       # CLI tool for scaffolding
```

## Testing Processes

To test an example process, navigate to the project root and run:

```bash
bun run counter:test
```

This command executes the test suite for the Counter process using Busted. For more detailed information about the testing framework, visit the [ao-process-testing repository](https://github.com/Autonomous-Finance/ao-process-testing).

## Building Processes

Building processes requires Docker to call the lua-squish image. Ensure that Docker is installed and running on your machine.

### Squishy File

Each process root directory must contain a `squishy` file with build instructions. Here's an example squishy file for the Counter process:

```
Main "src/process.lua"

Module "counter_lib" "./src/counter_lib.lua"

Option "minify-level" "none"
Output 'build/counter.lua'
```

### Build Command

To build an example process, run the following command from the project root:

```bash
bun run counter:build
```

The output will be written to `build/counter.lua`.

## Deploying Processes

Deployment is managed through [AOForm](https://github.com/Autonomous-Finance/aoform), a tool that deploys a set of processes to AO. Processes are defined in an `aoform.yaml` file, and AOForm uses a statefile to track deployed processes, only updating code when needed.

### Configuration File

The configuration file for a process (e.g., counter) is located at `./ao/counter/aoform.yaml`:

```yaml
- name: hello-world
  file: build/process.lua
  prerun: reset-modules.lua
  scheduler: _GQ33BkPtZrqxA84vM8Zk-N2aO0toNNu_C-l-rawrBA
  module: GYrbbe0VbHim_7Hi6zrOpHQXrSQz07XNtwCnfbFo2I0
  tags:
    - name: Hello World
      value: hello-world
```

### Deployment Steps

1. Set your wallet in the environment:
   ```bash
   export WALLET_JSON="$(cat ~/.aos.json)"
   ```

2. Run the deployment command:
   ```bash
   bun run counter:deploy
   ```

## Available Templates

The starter kit includes several templates:

- **Lua**: Basic Lua-based AO process template
- **Lua-SQLite**: Lua process with SQLite database support
- **Teal**: Teal-based AO process template
- **Teal-SQLite**: Teal process with SQLite database support

Each template includes:
- Pre-configured build scripts
- Example frontend application
- Testing setup
- Deployment configuration

## Documentation

Detailed documentation and further examples can be found in the `docs/` directory and the documentation site. The documentation covers:

- Getting started guides
- Process development architecture
- Frontend development
- Building and deployment
- Testing strategies

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Disclaimer

This project is archived and provided as-is. While the code is functional and may serve as a useful reference, users should:

- Review and update dependencies before use
- Test thoroughly in their own environment
- Be aware that some practices or dependencies may be outdated
- Consider forking and maintaining their own version if they plan to use it actively

## Acknowledgments

- [AO](https://ao.ar.io/) - The AO compute environment
- [AOForm](https://github.com/Autonomous-Finance/aoform) - Deployment tooling
- [Busted](https://olivinelabs.com/busted/) - Lua testing framework
