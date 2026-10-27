# Contributing

Thanks for helping improve mac-liuhai.

## Workflow

1. Fork `NIU-123370/mac-liuhai`.
2. Create a focused branch from `main`.
3. Build and test the change locally.
4. Open a pull request with a short description and screenshots for UI changes.

## Build and test

```sh
xcodebuild build \
  -project macLiuhai.xcodeproj \
  -scheme macLiuhai \
  -configuration Release \
  -destination "generic/platform=macOS"

swiftc -swift-version 5 \
  macLiuhai/models/AgentSession.swift \
  macLiuhai/managers/AgentStatusReader.swift \
  tests/agent-status/main.swift -o /tmp/agent-status-tests
/tmp/agent-status-tests
python3 tests/agent-status/test_hooks.py
```

Do not include credentials, prompts, tool output, or local machine identifiers in commits.

## Reports

Bug reports should include macOS version, mac-liuhai version, reproduction steps, and expected behavior. Feature requests should describe the user problem before the proposed implementation.
