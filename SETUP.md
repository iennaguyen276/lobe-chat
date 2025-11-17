# LobeChat Setup Guide

This guide will help you set up and configure LobeChat for local development or deployment.

## Prerequisites

- Node.js 18+ or Bun
- pnpm (recommended package manager)
- PostgreSQL (for server-side database features)

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/lobehub/lobe-chat.git
cd lobe-chat
```

### 2. Install Dependencies

```bash
pnpm install
```

### 3. Configure Environment Variables

Create a `.env.local` file in the root directory:

```bash
cp .env.local.example .env.local
```

Or use the pre-created `.env.local` file and update the following required variables:

```env
# Required: Your OpenAI API Key
OPENAI_API_KEY=sk-your-actual-api-key-here
```

### 4. Start Development Server

```bash
pnpm dev
# or
bun run dev
```

The application will be available at `http://localhost:3210`

## Configuration Options

### Basic Configuration

The `.env.local` file contains basic configuration for local development:

- `OPENAI_API_KEY`: Your OpenAI API key (required for AI functionality)
- `ACCESS_CODE`: Optional password to protect your application
- `OPENAI_PROXY_URL`: Optional proxy URL for OpenAI API
- `OPENAI_MODEL_LIST`: Optional custom model names

### Advanced Configuration

For more advanced configurations, refer to:

- `.env.example` - Full list of available environment variables
- `.env.example.development` - Development server configuration with Docker
- `.env.desktop` - Desktop application configuration

### AI Provider Configuration

LobeChat supports multiple AI providers. See `.env.example` for configuration options for:

- OpenAI
- Azure OpenAI
- Anthropic (Claude)
- Google AI
- AWS Bedrock
- Ollama (local models)
- And many more...

### Database Configuration

For server-side features with database:

```env
DATABASE_URL=postgresql://username:password@localhost:5432/lobechat
KEY_VAULTS_SECRET=your-secret-key
```

Generate a secure key using:
```bash
openssl rand -base64 32
```

### Authentication Configuration

For multi-user support with authentication:

```env
NEXT_PUBLIC_ENABLE_NEXT_AUTH=1
NEXT_AUTH_SECRET=your-secret-key
```

## Development Workflow

### Running Tests

```bash
# Run all tests
bun run test

# Run specific test file
bunx vitest run --silent='passed-only' 'path/to/test'
```

### Type Checking

```bash
bun run type-check
```

### Building for Production

```bash
bun run build
```

### Running Production Build

```bash
bun run start
```

## Desktop App Development

For desktop app development, use the `.env.desktop` configuration:

```bash
cp .env.desktop .env
bun run desktop:dev
```

## Docker Deployment

For Docker deployment:

```bash
docker-compose up -d
```

Or use the development Docker setup:

```bash
docker-compose -f docker-compose.development.yml up -d
```

## Troubleshooting

### API Key Issues

- Ensure your `OPENAI_API_KEY` is valid and has sufficient credits
- Check if you need to use a proxy URL for your region

### Build Issues

- Clear node_modules: `pnpm clean:node_modules`
- Reinstall dependencies: `pnpm install`

### Database Issues

- Ensure PostgreSQL is running
- Verify `DATABASE_URL` is correct
- Run migrations: `bun run db:migrate`

## Additional Resources

- [Official Documentation](https://lobehub.com/docs)
- [Contributing Guide](./CONTRIBUTING.md)
- [GitHub Issues](https://github.com/lobehub/lobe-chat/issues)

## Security Notes

- Never commit your `.env.local` file to version control
- Use strong, unique secrets for production deployments
- Regularly rotate API keys and secrets
- Review the security settings in `.env.example`
