# Shopify Auth Service

A production-ready, standalone OAuth authentication service for Shopify applications. This microservice provides secure, scalable authentication for Shopify apps with enterprise-grade security and clean architecture.


## 💡 The Need for this App

**The Challenge**: Managing multiple Shopify apps with different authentication systems is complex and time-consuming. Each app requires separate login processes, token management, and security configurations.

**The Solution**: This authentication service provides a unified, secure gateway for all your Shopify integrations. Instead of juggling multiple authentication flows, you get:

- **Single Sign-On Experience**: Authenticate once, access multiple services
- **Enhanced Security**: Enterprise-grade encryption and CSRF protection
- **Simplified Management**: Centralized token management and session handling
- **Reliable Integration**: Battle-tested OAuth 2.0 implementation

### How It Fulfills Your Needs

1. **Streamlined Access**: One authentication flow for all connected apps
2. **Secure by Default**: Your store's data is protected with industry-standard encryption
3. **Always Available**: Serverless architecture ensures 99.9% uptime
4. **Easy Integration**: Apps connect seamlessly without complex setup

---

## 🚀 Technical Overview

This service demonstrates modern backend architecture patterns and enterprise-ready implementation:

- **Serverless-First**: AWS Lambda deployment with auto-scaling
- **Type-Safe**: Full TypeScript implementation with Zod validation
- **Security-First**: AES-256-GCM encryption, CSRF protection, secure session management
- **Clean Architecture**: Separation of concerns with service layer pattern
- **Production Ready**: Comprehensive error handling, logging, and monitoring

### Architecture Highlights

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Client App    │───▶│  Auth Service    │───▶│   Shopify API   │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                              │
                              ▼
                       ┌──────────────────┐
                       │   DynamoDB       │
                       │ (Encrypted Tokens)│
                       └──────────────────┘
```

### Key Technical Features

- **OAuth 2.0 Implementation**: Complete flow with state parameter validation
- **Token Encryption**: AES-256-GCM encryption for stored tokens
- **Session Management**: Express sessions with secure configuration
- **Input Validation**: Zod schemas for all API inputs
- **Error Handling**: Comprehensive error responses with proper HTTP status codes
- **Security Headers**: Helmet.js for security headers
- **CORS Configuration**: Environment-aware CORS policies

### Code Quality Indicators

- **TypeScript**: Full type safety with strict configuration
- **ESLint**: Comprehensive linting rules with Prettier integration
- **Modular Design**: Clean separation of routes, services, and middleware
- **Error Boundaries**: Proper error handling at all levels
- **Documentation**: Inline JSDoc comments for all public methods

## 🔧 API Endpoints

### Authentication Flow
```http
GET /auth/shopify?shop=your-shop.myshopify.com
# Returns authorization URL for OAuth flow

GET /auth/shopify/callback
# Handles OAuth callback from Shopify

GET /auth/status
# Check current authentication status

GET /auth/token
# Retrieve access token for authenticated shop

POST /auth/logout
# Logout and revoke access
```

### System
```http
GET /health
# Service health check with uptime metrics
```

## 🛠 Setup & Deployment

### Prerequisites
- Node.js 22+ (LTS)
- AWS CLI configured
- Serverless Framework v4

### Quick Start

1. **Install Dependencies**
   ```bash
   npm install
   ```

2. **Configure Environment**
   ```bash
   # Set up AWS Parameter Store
   aws ssm put-parameter --name "/shopify-auth/SHOPIFY_CLIENT_ID" --value "your_client_id" --type "SecureString"
   aws ssm put-parameter --name "/shopify-auth/SHOPIFY_CLIENT_SECRET" --value "your_client_secret" --type "SecureString"
   aws ssm put-parameter --name "/shopify-auth/SHOPIFY_REDIRECT_URI" --value "your_redirect_uri" --type "SecureString"
   aws ssm put-parameter --name "/shopify-auth/SESSION_SECRET" --value "your_session_secret" --type "SecureString"
   aws ssm put-parameter --name "/shopify-auth/ENCRYPTION_KEY" --value "your_encryption_key" --type "SecureString"
   ```

3. **Deploy**
   ```bash
   npm run deploy
   ```

### Development
```bash
npm run dev          # Start development server
npm run offline      # Test with serverless-offline
npm run lint         # Run ESLint
npm run test         # Run test suite
```

## 🔒 Security Features

- **Encrypted Storage**: All tokens encrypted with AES-256-GCM
- **CSRF Protection**: State parameter validation
- **Secure Sessions**: HttpOnly cookies with secure flags
- **Input Validation**: Zod schemas prevent injection attacks
- **Environment Isolation**: Sensitive data in AWS Parameter Store
- **IAM Roles**: Least privilege access patterns

## 📊 Performance & Scalability

- **Serverless Architecture**: Auto-scaling based on demand
- **Cold Start Optimization**: Lazy service initialization
- **Connection Pooling**: Efficient DynamoDB connections
- **Response Caching**: Strategic caching for token retrieval
- **Monitoring**: CloudWatch integration for observability

## 🧪 Testing

```bash
npm run test         # Run integration tests
npm run test:unit    # Run unit tests (if implemented)
```

## 📈 Monitoring & Observability

- **Health Checks**: Comprehensive health endpoint
- **Error Logging**: Structured error logging
- **Performance Metrics**: Response time tracking
- **Security Monitoring**: Failed authentication attempts

## 🏗 Infrastructure

- **AWS Lambda**: Serverless compute
- **DynamoDB**: Encrypted token storage with TTL
- **AWS Parameter Store**: Secure configuration management
- **CloudWatch**: Logging and monitoring
- **API Gateway**: HTTP endpoint management

## 📝 License

MIT License - see LICENSE file for details

---

**Built with**: TypeScript, Express.js, AWS Lambda, DynamoDB, Serverless Framework v4

**Node.js Version**: 22+ (LTS)