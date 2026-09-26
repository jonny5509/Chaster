# Contributing

Thank you for your interest in contributing! Contributions, bug reports, feature requests, documentation improvements, and code reviews are welcome.

## Before You Start

- Read the repository's [Code of Conduct](CODE_OF_CONDUCT.md).
- Check existing issues and pull requests before opening a new one.
- For security vulnerabilities, follow the instructions in [SECURITY.md](SECURITY.md) and do not disclose sensitive details publicly.
- Keep changes focused and avoid unrelated modifications.

## Reporting Bugs

Please use the **Bug Report** issue template and include:

- Integration version
- Home Assistant version
- Steps to reproduce
- Expected and actual behaviour
- Relevant logs or error messages
- Any useful configuration or device/API details

Remove passwords, tokens, personal information, and other sensitive data before posting.

## Requesting Features

Use the **Feature Request** issue template. Explain the problem or use case, the proposed behaviour, and any alternatives or workarounds you have considered.

## Development

1. Fork the repository or create a working branch.
2. Make your changes in a focused branch.
3. Follow the existing project structure and coding conventions.
4. Update documentation when behaviour, configuration, or setup changes.
5. Test your changes with a supported Home Assistant installation where practical.
6. Review your changes for accidental secrets, debug code, or unrelated files.
7. Commit your changes with a clear message.
8. Open a pull request using the repository's pull request template.

## Pull Requests

Please provide:

- A clear description of the change and its motivation.
- Links to related issues where applicable.
- Testing details, including Home Assistant and integration versions when relevant.
- Documentation updates when needed.
- Any compatibility or migration considerations.

Pull requests should be focused, reviewable, and limited to the intended change.

## Code Quality

- Prefer small, maintainable changes.
- Follow the style and patterns already used in the repository.
- Avoid unnecessary dependencies.
- Do not commit secrets, credentials, personal data, generated local files, or environment-specific configuration.
- Preserve backwards compatibility where practical.
- Add or update tests when appropriate.

## Home Assistant Changes

For changes affecting Home Assistant entities, services, configuration, devices, or integrations:

- Verify the integration loads without errors.
- Test affected functionality.
- Check relevant logs for warnings and errors.
- Update the README or other documentation if user-facing behaviour changes.

## Versioning and Releases

Do not change the integration version unless the change is intended to be part of a release. Follow the existing release/versioning approach used by the repository.

## Review Process

Maintainers may request changes, clarification, additional testing, or documentation before merging a contribution. Please respond to review feedback and keep follow-up commits focused.

By contributing, you agree that your contributions will be made under the repository's existing license and that you will follow the project's Code of Conduct.
