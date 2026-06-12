---
aliases: []
tags: []
date created: Friday, April 24th 2026, 6:15:14 am
date modified: Thursday, May 21st 2026, 3:03:38 pm
---

# Backend Tests

## Structure

```
tests/
├── e2e/
│   ├── config.py         # Test configuration
│   ├── conftest.py       # Pytest fixtures
│   ├── requirements.txt  # Dependencies
│   └── smoke/           # E2E test files
├── unit/                # Unit tests (future)
└── integration/         # Integration tests (future)
```

## Run E2E Tests

```bash
cd tests/e2e
pip install -r requirements.txt

# Create .env.test with your credentials

# Run tests
pytest smoke/
```

See [e2e/README.md](e2e/README.md) for details.
