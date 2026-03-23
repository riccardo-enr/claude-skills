# ROS 2 Conventions Checklist

Condensed from official ROS 2 Jazzy documentation. Each item links to its source.

## Package Structure
Source: [Developer Guide](https://docs.ros.org/en/jazzy/The-ROS2-Project/Contributing/Developer-Guide.html)

- [ ] `package.xml` follows REP-0140 format
- [ ] Package name: lowercase, starts with letter, underscores only, descriptive (not generic like "utils")
- [ ] No `ros` prefix unless core package
- [ ] Complete metadata: `<description>`, `<maintainer>`, `<license>`, `<url>`
- [ ] All runtime/build/test dependencies declared
- [ ] `CHANGELOG.rst` present (REP-0132)
- [ ] `LICENSE` file present
- [ ] `README` present with description, build instructions, examples

### File layout

```
<package>/
├── include/<package>/   # public C/C++ headers (namespaced)
├── src/                 # C/C++ sources + private headers
├── <package>/           # Python modules
├── test/                # tests + test data
├── config/              # YAML configs, RViz configs
├── launch/              # launch files
├── msg/                 # message definitions
├── srv/                 # service definitions
├── action/              # action definitions
├── package.xml
├── CMakeLists.txt       # (ament_cmake)
├── setup.py             # (ament_python)
├── README
├── LICENSE
└── CHANGELOG.rst
```

## CMakeLists.txt (ament_cmake)
Source: [ament_cmake docs](https://docs.ros.org/en/jazzy/How-To-Guides/Ament-CMake-Documentation.html)

- [ ] `cmake_minimum_required(VERSION 3.8)`
- [ ] `project()` name matches `package.xml` name
- [ ] C++17 standard set explicitly
- [ ] Compiler warnings: `-Wall -Wextra -Wpedantic` for GCC/Clang
- [ ] `find_package()` for explicit deps only (no transitive)
- [ ] Use `ament_target_dependencies()` or namespaced `target_link_libraries()` (e.g., `Eigen3::Eigen`)
- [ ] Headers: `target_include_directories()` with `BUILD_INTERFACE` and `INSTALL_INTERFACE`
- [ ] Install headers to `include/${PROJECT_NAME}`
- [ ] Install executables to `lib/${PROJECT_NAME}`
- [ ] Install libraries with proper export set (name differs from target)
- [ ] `ament_export_targets()` with `HAS_LIBRARY_TARGET` for libraries
- [ ] `ament_export_dependencies()` for transitive deps
- [ ] `ament_package()` called exactly once, as the **last** CMake command
- [ ] CMake style: lowercase commands, snake_case identifiers, 2-space indent, empty `else()`/`endif()`

### Anti-patterns
- Calling ament commands from CMake subdirectories
- Omitting `HAS_LIBRARY_TARGET`
- Mixing target-based and non-target exports
- Finding transitive dependencies unnecessarily

## C++ Code Style
Source: [Code Style guide](https://docs.ros.org/en/jazzy/The-ROS2-Project/Contributing/Code-Style-Language-Versions.html)

- [ ] File extensions: `.hpp` for headers, `.cpp` for sources
- [ ] Max 100 characters per line
- [ ] 2-space indentation (no tabs)
- [ ] Classes/types: `PascalCase`
- [ ] Functions/variables: `snake_case`
- [ ] Global variables: `g_` prefix + snake_case
- [ ] Always use braces after `if`, `else`, `do`, `while`, `for`
- [ ] Open braces for function/class definitions; cuddle braces for control flow
- [ ] Nested templates: no whitespace (`set<list<string>>`)
- [ ] Documentation: `///` or `/** */` (Doxygen-compatible)
- [ ] C++17 target (Jazzy)
- [ ] Avoid Boost unless absolutely required
- [ ] Do not use `std::shared_ptr` by reference (undermines refcounting)
- [ ] Avoid streaming to `stdout`/`stderr` directly (thread interleaving)
- [ ] Exceptions allowed; avoid in destructors

### Linting tools
- `ament_clang_format`
- `ament_cpplint`
- `ament_uncrustify`
- `ament_cppcheck`

## Python Code Style
Source: [Code Style guide](https://docs.ros.org/en/jazzy/The-ROS2-Project/Contributing/Code-Style-Language-Versions.html)

- [ ] Python 3 only
- [ ] Max 100 characters per line
- [ ] Single quotes preferred (unless escaping needed)
- [ ] One import per line
- [ ] Hanging indents for continuation lines
- [ ] PEP 8 compliant

### Linting tools
- `ament_pycodestyle`

## Node Design
Source: [Composition tutorial](https://docs.ros.org/en/jazzy/Tutorials/Intermediate/Composition.html)

- [ ] Constructor accepts `const rclcpp::NodeOptions&` for composability
- [ ] `RCLCPP_COMPONENTS_REGISTER_NODE` macro for component registration
- [ ] Consider lifecycle nodes for drivers/hardware (state machine: unconfigured → inactive → active)
- [ ] Document callback groups and executor choice

## Parameters
Source: [Parameters concept](https://docs.ros.org/en/jazzy/Concepts/Basic/About-Parameters.html)

- [ ] All parameters declared at startup via `declare_parameter()`
- [ ] Parameter descriptors with descriptions and value ranges
- [ ] Type safety enabled (default) — no `allow_undeclared_parameters` without justification
- [ ] Use parameter callbacks for validation (pre-set: no side effects; post-set: safe for side effects)
- [ ] No hardcoded values that should be configurable

## Quality of Service
Source: [QoS docs](https://docs.ros.org/en/jazzy/Concepts/Intermediate/About-Quality-of-Service-Settings.html)

- [ ] Sensor streams → `SensorDataQoS` (best-effort, small queue)
- [ ] Reliable commands → reliable profile
- [ ] Services → services profile (reliable + volatile)
- [ ] Pub/sub QoS profiles must be compatible (incompatible = silent disconnection)
- [ ] Transient local durability for latching behavior
- [ ] Explicit QoS selection documented/justified

## Logging
Source: [Logging docs](https://docs.ros.org/en/jazzy/Concepts/Intermediate/About-Logging.html)

- [ ] Use `RCLCPP_{DEBUG,INFO,WARN,ERROR,FATAL}` macros, not `std::cout`/`printf`/`std::cerr`
- [ ] Use `_THROTTLE` variants for high-frequency diagnostics
- [ ] Use `_ONCE` for startup/shutdown messages
- [ ] Logger obtained via `node->get_logger()`
- [ ] Severity levels: DEBUG for development, INFO for operation, WARN for concerning, ERROR for failures, FATAL for critical

## Launch Files
Source: [Launch best practices](https://docs.ros.org/en/jazzy/Tutorials/Intermediate/Launch/Using-ROS2-Launch-For-Large-Projects.html)

- [ ] File suffix: `_launch.py`, `_launch.xml`, or `_launch.yaml`
- [ ] Modular: top-level launch includes sub-launches
- [ ] Use `find-pkg-share` for paths (not hardcoded)
- [ ] Extract parameters to YAML when >3-4 params
- [ ] Namespace management via `PushROSNamespace` in `GroupAction`
- [ ] Use `DeclareLaunchArgument` with defaults for configurable values

## Naming Conventions
Source: [Developer Guide](https://docs.ros.org/en/jazzy/The-ROS2-Project/Contributing/Developer-Guide.html)

- [ ] Packages: lowercase, underscores, descriptive
- [ ] Topics/services/actions: `snake_case`
- [ ] Nodes: `snake_case`
- [ ] Frames: follow REP-0105 conventions

## Testing
Source: [Developer Guide](https://docs.ros.org/en/jazzy/The-ROS2-Project/Contributing/Developer-Guide.html), [ament_cmake docs](https://docs.ros.org/en/jazzy/How-To-Guides/Ament-CMake-Documentation.html)

- [ ] All test code wrapped in `if(BUILD_TESTING)`
- [ ] `ament_lint_auto` + `ament_lint_common` in test dependencies
- [ ] `ament_add_gtest` for C++ tests (not raw `add_test`)
- [ ] Unit tests present at minimum
- [ ] Line coverage ≥95% for core packages
- [ ] Separate packages for system tests (avoid circular deps)

## General
Source: [Developer Guide](https://docs.ros.org/en/jazzy/The-ROS2-Project/Contributing/Developer-Guide.html)

- [ ] Declare variables in narrowest scope
- [ ] Keep groups (deps, imports, includes) alphabetically ordered
- [ ] All error messages to stderr
- [ ] Check return codes / throw on failure (defensive programming)
- [ ] License and copyright in every source file
- [ ] Units follow REP-0103