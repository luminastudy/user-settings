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

This package uses [release-it](https://github.com/release-it/release-it) for automated releases. Releases are managed through GitHub Actions.

#### Local Release (requires maintainer access)

```bash
# Dry run to see what would happen
pnpm run release:dry

# Create a patch release (0.1.0 -> 0.1.1)
pnpm run release patch

# Create a minor release (0.1.0 -> 0.2.0)
pnpm run release minor

# Create a major release (0.1.0 -> 1.0.0)
pnpm run release major
```

#### CI/CD Release

1. Go to the [Actions tab](https://github.com/luminastudy/user-settings/actions)
2. Select the "Release" workflow
3. Click "Run workflow"
4. Choose the version increment (patch/minor/major)
5. Click "Run workflow"

This will:
- Run tests
- Build the package
- Bump the version
- Update CHANGELOG.md
- Create a git commit and tag
- Create a GitHub release
- Publish to npm

## License

MIT
