# Contributing

Thanks for your interest. Small, focused pull requests are easiest to review.

## Setup

```bash
git clone https://github.com/<your-username>/smart-wifi-antenna.git
cd smart-wifi-antenna
python -m venv .venv && source .venv/bin/activate
pip install -r requirements-dev.txt
pip install -e .
```

You do not need a Raspberry Pi to develop. Use `smart-antenna --simulate`.

## Before you open a pull request

```bash
ruff check .
pytest
```

Both must pass. CI runs the same checks.

## Guidelines

- One change per pull request. Explain what and why.
- Add or update tests for any behaviour change.
- Keep hardware code (GPIO, LCD) behind the `Rotor` and `Display` classes so it stays testable.
- Update `CHANGELOG.md` under **Unreleased**.
- Do not commit `config.yaml`, recordings, or any network names or passwords.

## Reporting bugs

Open an issue with: what you expected, what happened, your Pi model, OS version, Python version, and the log output (`log_level: DEBUG`).

## Code of conduct

Be respectful. Disagree with ideas, not people.
