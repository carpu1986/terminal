# GitHub Copilot Instructions for Windows Terminal

## Programming Languages and Frameworks

This project primarily uses:
- **C++17/C++20**: Core console host and terminal components
- **C++/WinRT**: Windows Terminal application (UWP/XAML components)
- **C#**: Supporting tools and utilities
- **XAML**: User interface markup

## Coding Standards

### C++ Style Guidelines

1. **Follow Modern C++**: Reference the [C++ Core Guidelines](https://github.com/isocpp/CppCoreGuidelines) for new code
2. **Consistency First**: When modifying existing code, match the existing style
3. **Smart Pointers**: Use [Windows Implementation Library (WIL)](https://github.com/Microsoft/wil) for Win32/NT/COM APIs
4. **Result Handling**: 
   - Prefer HRESULT or exceptions over NTSTATUS
   - Functions returning status codes should be marked `noexcept` and have `[[nodiscard]]` attribute
   - Avoid returning status codes for functions that always succeed

### C++/WinRT Guidelines

- Use appropriate [strong and weak references](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/weak-references) in TerminalApp
- Understand [concurrency schemes](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) when working with async operations

## Project Organization

- Place unit tests in `ut_` folders (e.g., `ut_host`)
- Place functional tests in `ft_` folders (e.g., `ft_api`)
- Place interfaces in `inc` folders
- Package new components as libraries with well-defined interfaces
- Follow existing project structure patterns

## Architecture

### Key Components

- **Console Host** (`src/host`): Windows Console infrastructure and API server
- **Terminal Core** (`src/cascadia/TerminalCore`): Core terminal buffer and VT parsing
- **Terminal Control** (`src/cascadia/TerminalControl`): UWP-XAML terminal UI control
- **Terminal App** (`src/cascadia/TerminalApp`): Windows Terminal application logic
- **Renderer** (`src/renderer`): Text rendering abstraction with multiple backends (GDI, DirectWrite)
- **Virtual Terminal** (`src/terminal`): VT sequence parser and adapter

## Testing

- Use TAEF (Test Authoring and Execution Framework) as the primary testing framework
- Write unit tests for all new functionality
- Ensure tests are placed in appropriate `ut_` or `ft_` directories
- Follow existing test patterns and structure

## General Practices

- Maintain backward compatibility where required
- Use STL containers for modern code
- Avoid home-grown collections in new code
- Keep memory usage and performance in mind
- Write clear, maintainable code that others can understand
- Document complex logic and non-obvious design decisions
