# API Credentials and Security Guide

This document provides comprehensive details on the API credentials required for SamFamilyTreeWeb, how to obtain them, and best practices for secure credential management.

## Required API Credentials

### Google Maps Platform

#### Services Used
- **Maps JavaScript API**: For rendering interactive maps
- **Geocoding API**: For converting place names to coordinates
- **Places API**: For place autocomplete functionality

#### How to Obtain Credentials
1. Create a Google Cloud Platform account at [https://console.cloud.google.com/](https://console.cloud.google.com/)
2. Create a new project specifically for SamFamilyTreeWeb
3. Enable the Maps JavaScript API, Geocoding API, and Places API
4. Create an API key:
   - Go to "Credentials" in the left sidebar
   - Click "Create Credentials" → "API Key"
   - For security, restrict the API key:
     - Restrict to HTTP referrers (your website domains)
     - Restrict to specific APIs (only the three APIs mentioned above)

#### Configuration
- Set billing alerts to avoid unexpected charges
- Monitor usage in the Google Cloud Console
- Start with a free tier to test functionality

### Dialogflow (Google Cloud)

#### Services Used
- **Dialogflow CX**: For advanced conversational chatbot functionality
- **Dialogflow API**: For integrating the chatbot with the application

#### How to Obtain Credentials
1. In Google Cloud Console, enable the Dialogflow API
2. Create a new Dialogflow agent:
   - Go to [https://dialogflow.cloud.google.com/](https://dialogflow.cloud.google.com/)
   - Click "Create Agent"
   - Configure the agent settings
3. Create a service account:
   - Go to "IAM & Admin" → "Service Accounts" in Google Cloud Console
   - Create a new service account with "Dialogflow API Client" role
   - Create and download a JSON key file

#### Configuration
- Import intents and entities from backup files (if available)
- Train the model with sample conversations

### PostgreSQL Database

#### Services Used
- **PostgreSQL**: Primary database for all family tree data
- **PostGIS Extension**: For geographical data support

#### Credentials Needed
- **Host**: Database server hostname or IP
- **Port**: Usually 5432 for PostgreSQL
- **Username**: Database user with appropriate permissions
- **Password**: Secure password for the database user
- **Database Name**: Name of the specific database for the application

#### Configuration
- Use strong, unique passwords
- Create a dedicated user with limited permissions for the application
- Enable TLS/SSL for secure connections

### AWS S3 (or compatible service)

#### Services Used
- **S3 Buckets**: For storing user-uploaded photos and exported SVG files

#### How to Obtain Credentials
1. Create an AWS account at [https://aws.amazon.com/](https://aws.amazon.com/)
2. Create an IAM user specifically for SamFamilyTreeWeb:
   - Go to IAM in the AWS Management Console
   - Create a new user with programmatic access
   - Attach only the necessary S3 permissions
3. Create and download access keys for the IAM user
4. Create an S3 bucket for the application

#### Configuration
- Configure CORS to allow uploads from your domains
- Set appropriate bucket policies
- Consider implementing lifecycle rules for cost optimization

## Optional API Credentials

### OpenAI API (for AI features)

#### Services Used
- **GPT API**: For advanced text analysis and generation

#### How to Obtain Credentials
1. Create an OpenAI account at [https://openai.com/](https://openai.com/)
2. Subscribe to an appropriate plan
3. Generate an API key from the dashboard

#### Configuration
- Set usage limits to control costs
- Monitor token usage

### Genealogy Services APIs

#### Potential Services
- **FamilySearch API**: Access to genealogical records
- **Ancestry API**: If partnership is established
- **MyHeritage API**: For additional data sources

#### How to Obtain Credentials
- Each service has a different application process
- Generally requires registering as a developer and applying for access

## Environment Variables Setup

### Development Environment

Create a `.env` file in the root directory with the following structure:

```
# Google Maps
REACT_APP_GOOGLE_MAPS_API_KEY=your_api_key_here

# Dialogflow
REACT_APP_DIALOGFLOW_PROJECT_ID=your_project_id
GOOGLE_APPLICATION_CREDENTIALS=path/to/service-account-key.json

# Database
DB_HOST=localhost
DB_PORT=5432
DB_USER=your_db_user
DB_PASSWORD=your_db_password
DB_NAME=family_history_db

# Storage
S3_BUCKET=your_bucket_name
S3_REGION=your_region
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key

# Optional APIs
OPENAI_API_KEY=your_openai_key
```

### Production Environment

For production, set these values:
- In your hosting provider's environment variables section
- Using a secrets management service
- During CI/CD deployment process

## Security Best Practices

### API Key Protection
- **NEVER commit API keys to version control**
- Use environment variables for all credentials
- Implement API key restrictions where possible (domain, IP, service)
- Set up key rotation policies

### Frontend Security
- Store only public API keys in frontend code (with API restrictions)
- Use backend proxies for sensitive API calls
- Implement proper CORS headers on all services

### Backend Security
- Validate all inputs
- Implement rate limiting
- Use secure headers (HTTPS, Content-Security-Policy, etc.)
- Keep dependencies updated

### Database Security
- Use parameterized queries to prevent SQL injection
- Encrypt sensitive data at rest
- Implement proper access controls
- Regularly backup the database

### Monitoring and Auditing
- Enable activity logging for all services
- Set up alerts for unusual API usage
- Conduct regular security reviews
- Have an incident response plan

## Credential Rotation Schedule

| Credential Type | Rotation Frequency | Responsible Party |
|-----------------|------------------- |------------------- |
| Google Maps API Key | Every 6 months | DevOps Lead |
| Database Passwords | Every 3 months | Database Admin |
| AWS Access Keys | Every 3 months | Cloud Admin |
| Dialogflow SA Keys | Every 6 months | AI Integration Lead |

## Handling Credential Exposure

If you suspect credentials have been exposed:
1. Immediately revoke and replace the affected credentials
2. Audit all access logs for unauthorized usage
3. Document the incident and update security practices
4. Check for any data breaches resulting from the exposure

Remember: Treat all credentials with the highest security precautions. Never share credentials through insecure channels like email or chat applications.