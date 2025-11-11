# @lumina-study/user-settings

JSON schema and TypeScript types for Lumina Study user settings configuration.

## Installation

```bash
pnpm add @lumina-study/user-settings
# or
npm install @lumina-study/user-settings
```

## Usage

### Using the JSON Schema

```javascript
const schema = require('@lumina-study/user-settings');

// Use for validation with libraries like ajv
const Ajv = require('ajv');
const ajv = new Ajv();
const validate = ajv.compile(schema);

const userSettings = {
  language: 'en',
  degreeId: 'degree-123'
};

const valid = validate(userSettings);
if (!valid) {
  console.error(validate.errors);
}
```

### Using TypeScript Types

```typescript
import type { UserSettings } from '@lumina-study/user-settings';

const settings: UserSettings = {
  language: 'en',
  degreeId: 'degree-123'
};
```

## Schema

The user settings schema includes the following properties:

- **language** (required): User interface language
  - Type: `string`
  - Allowed values: `"he"`, `"en"`
  - Default: `"en"`

- **degreeId** (optional): User's degree identifier
  - Type: `string | null`
  - Default: `null`

## Development

### Building

```bash
pnpm install
pnpm run build
```

This will generate TypeScript types from the JSON schema.

### Publishing

This package uses [release-it](https://github.com/release-it/release-it) for automated releases.

#### Automatic Release (on push to main)

**Every push to the `main` branch automatically triggers a patch release** (e.g., 0.1.0 → 0.1.1).

The workflow will:
- Run tests
- Build the package
- Bump the patch version
- Update CHANGELOG.md
- Create a git commit and tag
- Create a GitHub release
- Publish to npm

**Note:** Release commits from github-actions[bot] are automatically skipped to prevent infinite loops.

#### Manual Release (for minor/major versions)

To create a minor or major release:

1. Go to the [Actions tab](https://github.com/luminastudy/user-settings/actions)
2. Select the "Release" workflow
3. Click "Run workflow"
4. Choose the version increment:
   - **patch** (0.1.0 → 0.1.1) - Bug fixes
   - **minor** (0.1.0 → 0.2.0) - New features
   - **major** (0.1.0 → 1.0.0) - Breaking changes
5. Click "Run workflow"

#### Local Release (requires maintainer access)

```bash
# Dry run to see what would happen
pnpm run release:dry

# Create a specific release
pnpm run release patch   # 0.1.0 -> 0.1.1
pnpm run release minor   # 0.1.0 -> 0.2.0
pnpm run release major   # 0.1.0 -> 1.0.0
```

## License

MIT
