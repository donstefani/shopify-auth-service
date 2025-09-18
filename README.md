# Shopify Auth Service

A clean, standalone OAuth authentication service for Shopify applications.

## Features

- **OAuth 2.0 Flow**: Complete Shopify OAuth implementation
- **Secure Token Storage**: Encrypted tokens in DynamoDB with TTL
- **Session Management**: Secure session handling with CSRF protection
- **Serverless**: Deployed on AWS Lambda with serverless-http
- **Clean Architecture**: Simplified, maintainable codebase

## API Endpoints

### Authentication
- `GET /auth/shopify?shop=your-shop.myshopify.com` - Initiate OAuth flow
- `GET /auth/shopify/callback` - Handle OAuth callback
- `GET /auth/status` - Check authentication status
- `GET /auth/token` - Get access token
- `POST /auth/logout` - Logout and revoke access

### Health Check
- `GET /health` - Service health status

## Setup

1. **Install dependencies**:
   ```bash
   npm install
   ```

2. **Configure environment**:
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

3. **Set up AWS Parameter Store**:
   ```bash
   aws ssm put-parameter --name "/shopify-auth/SHOPIFY_CLIENT_ID" --value "your_client_id" --type "SecureString"
   aws ssm put-parameter --name "/shopify-auth/SHOPIFY_CLIENT_SECRET" --value "your_client_secret" --type "SecureString"
   aws ssm put-parameter --name "/shopify-auth/SHOPIFY_REDIRECT_URI" --value "your_redirect_uri" --type "SecureString"
   aws ssm put-parameter --name "/shopify-auth/SESSION_SECRET" --value "your_session_secret" --type "SecureString"
   aws ssm put-parameter --name "/shopify-auth/ENCRYPTION_KEY" --value "your_encryption_key" --type "SecureString"
   ```

4. **Deploy**:
   ```bash
   npm run deploy
   ```

## Development

```bash
npm run dev          # Start development server
npm run offline      # Test with serverless-offline
npm run lint         # Run ESLint
```

## Architecture

This service provides a clean, focused OAuth implementation that other Shopify apps can consume. It handles:

- OAuth flow initiation and callback processing
- Secure token storage with encryption
- Session management for web applications
- Token retrieval and revocation

## Security

- All sensitive data stored in AWS Parameter Store
- Tokens encrypted with AES-256-GCM
- CSRF protection with state parameters
- Secure session configuration
- Input validation with Zod schemas
