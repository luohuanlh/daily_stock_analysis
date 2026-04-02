```markdown
# daily_stock_analysis Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches the core development patterns, coding conventions, and collaborative workflows used in the `daily_stock_analysis` repository. The project is a Python-based stock analysis application, built with Flask for the backend and a TypeScript/React frontend. The repository emphasizes clear commit conventions, modular code structure, comprehensive testing, and robust documentation practices. By following these patterns, contributors can efficiently add features, fix bugs, refactor code, and maintain high code quality across both backend and frontend.

## Coding Conventions

### File Naming
- Use **snake_case** for all Python files and modules.
  - Example: `data_provider/stock_fetcher.py`, `src/services/user_service.py`
- TypeScript/React files use **PascalCase** for components and **snake_case** for utility files.
  - Example: `StockChart.tsx`, `api_client.ts`

### Import Style
- **Python:** Use **relative imports** within packages.
  ```python
  from .models import StockModel
  from ..utils import parse_date
  ```
- **TypeScript:** Use relative imports for local modules.
  ```typescript
  import { fetchStockData } from '../api/stock_api';
  ```

### Export Style
- **Python:** Use **named exports** (explicitly define what is exported).
  ```python
  def analyze_stock(...):
      ...
  __all__ = ['analyze_stock']
  ```
- **TypeScript:** Use named exports.
  ```typescript
  export function fetchStockData(...) { ... }
  ```

### Commit Messages
- Follow **Conventional Commits** with these prefixes: `fix`, `feat`, `docs`, `chore`, `[feat]`
- Keep commit messages concise (average ~55 characters).
  - Example: `feat: add endpoint for historical stock data`

## Workflows

### Feature Development: API, Frontend, Backend, Test & Doc
**Trigger:** When adding a new user-facing feature that requires backend, API, frontend, and documentation updates.  
**Command:** `/new-feature`

1. Add or update API endpoint (`api/v1/endpoints/*.py`, `api/v1/schemas/*.py`)
2. Implement or update backend service logic (`src/services/*.py`, `src/repositories/*.py`)
3. Update or create frontend API client/types (`apps/dsa-web/src/api/*.ts`, `apps/dsa-web/src/types/*.ts`)
4. Update or create frontend UI components/pages (`apps/dsa-web/src/pages/*.tsx`, `apps/dsa-web/src/components/**/*.tsx`)
5. Write or update tests for backend (`tests/test_*.py`) and frontend (`apps/dsa-web/src/pages/__tests__/*.test.tsx`, `apps/dsa-web/src/components/**/__tests__/*.test.tsx`)
6. Update documentation and changelog (`docs/CHANGELOG.md`, `README.md`, `docs/README_EN.md`, `docs/full-guide.md`)

**Example:**
```python
# api/v1/endpoints/stock.py
from flask import Blueprint
from .schemas import StockSchema

@stock_bp.route('/api/v1/stock', methods=['POST'])
def add_stock():
    ...
```
```typescript
// apps/dsa-web/src/api/stock_api.ts
export async function addStock(data: StockInput) { ... }
```

---

### Bugfix: Backend Service, Test & Changelog
**Trigger:** When fixing a bug in backend services or core logic.  
**Command:** `/bugfix`

1. Fix or update backend code (`src/**/*.py`, `data_provider/**/*.py`, `main.py`)
2. Update or add relevant tests (`tests/test_*.py`)
3. Update documentation and changelog (`docs/CHANGELOG.md`, `docs/README_*.md`)

**Example:**
```python
# src/services/stock_service.py
def get_stock_data(...):
    # Fixed edge case for missing data
    ...
```

---

### Frontend UI Refactor or Polish (with Tests)
**Trigger:** When improving, refactoring, or unifying frontend UI/UX or component structure.  
**Command:** `/refactor-ui`

1. Refactor or update frontend components/pages (`apps/dsa-web/src/components/**/*.tsx`, `apps/dsa-web/src/pages/*.tsx`)
2. Update or add frontend tests (`apps/dsa-web/src/components/**/__tests__/*.test.tsx`, `apps/dsa-web/src/pages/__tests__/*.test.tsx`)
3. Update global styles or shared utilities if needed (`apps/dsa-web/src/index.css`, `apps/dsa-web/src/utils/*.ts`)
4. Update documentation and changelog (`docs/CHANGELOG.md`)

**Example:**
```tsx
// apps/dsa-web/src/components/StockCard/StockCard.tsx
export function StockCard({ stock }) { ... }
```

---

### Add or Update Configuration or ENV Support
**Trigger:** When introducing or modifying configuration/environment variables or system settings.  
**Command:** `/update-config`

1. Update configuration files (`.env.example`, `src/config.py`, `src/core/config_registry.py`)
2. Update or add related backend logic (`src/services/system_config_service.py`)
3. Update or add tests for configuration (`tests/test_config_*.py`, `tests/test_system_config_*.py`)
4. Update documentation and changelog (`docs/CHANGELOG.md`, `docs/README_*.md`, `docs/full-guide*.md`)

**Example:**
```python
# src/config.py
import os
DATABASE_URL = os.getenv('DATABASE_URL', 'sqlite:///default.db')
```

---

### Add or Update Tests for Existing Feature
**Trigger:** When improving test coverage or updating tests after code changes.  
**Command:** `/add-tests`

1. Add or update backend tests (`tests/test_*.py`)
2. Add or update frontend tests (`apps/dsa-web/src/pages/__tests__/*.test.tsx`, `apps/dsa-web/src/components/**/__tests__/*.test.tsx`)
3. Update documentation and changelog if needed (`docs/CHANGELOG.md`)

**Example:**
```python
# tests/test_stock_service.py
def test_get_stock_data_returns_expected_result():
    ...
```

---

### Changelog or Docs Release Preparation
**Trigger:** When preparing for a release or reorganizing documentation/changelog after many changes.  
**Command:** `/prepare-release-docs`

1. Update `docs/CHANGELOG.md` (add, reorganize, or clean up entries)
2. Update other documentation files as needed (`README.md`, `docs/README_*.md`, `docs/full-guide*.md`)

**Example:**
```markdown
## [1.2.0] - 2024-06-10
### Added
- New endpoint for batch stock import
```

---

## Testing Patterns

- **Backend (Python):**  
  - Tests are in `tests/` directory, named as `test_*.py`.
  - Use standard Python testing frameworks (e.g., pytest).
  - Example:
    ```python
    def test_analyze_stock_returns_expected_value():
        ...
    ```

- **Frontend (TypeScript/React):**  
  - Tests use **vitest**.
  - Test files follow the pattern: `*.test.tsx` and are placed under `__tests__` directories.
  - Example:
    ```typescript
    // apps/dsa-web/src/components/StockCard/__tests__/StockCard.test.tsx
    import { render } from '@testing-library/react';
    import { StockCard } from '../StockCard';

    test('renders stock name', () => {
      ...
    });
    ```

## Commands

| Command               | Purpose                                                      |
|-----------------------|--------------------------------------------------------------|
| /new-feature          | Start a new feature spanning API, backend, frontend & docs   |
| /bugfix               | Fix a bug in backend logic and update tests/docs             |
| /refactor-ui          | Refactor or polish frontend UI with tests                    |
| /update-config        | Add or update configuration/environment support              |
| /add-tests            | Add or update tests for existing features                    |
| /prepare-release-docs | Prepare or update changelog and documentation for release    |
```