# AI Engineering Studio - Environment Configuration

## Development Setup

```bash
# Install dependencies
npm install

# Setup environment variables
cp .env.example .env.local

# Run development server
npm run dev

# Run with Docker Compose
docker-compose up -d
```

## Production Deployment - Railway

### Prerequisites
- Railway account (https://railway.app)
- GitHub repository connected to Railway
- Environment variables configured

### Environment Variables Required

```
NODE_ENV=production
PORT=3000
LOG_LEVEL=info

# Database
DATABASE_URL=postgresql://user:password@host:5432/dbname
REDIS_URL=redis://host:6379

# API Keys (if needed)
OPENAI_API_KEY=sk-...
HUGGINGFACE_API_KEY=hf_...
```

### Deployment Steps

1. **Connect Repository to Railway**
   ```
   Visit https://railway.app/new
   Select "GitHub Repo"
   Authorize and select muhaksdar11-hub/ai-engineering-studio
   ```

2. **Configure Environment**
   - Add environment variables in Railway dashboard
   - Set `NODE_ENV` to `production`

3. **Database Setup**
   ```bash
   # Create PostgreSQL plugin in Railway
   # Create Redis plugin in Railway
   # Copy DATABASE_URL and REDIS_URL to environment
   ```

4. **Deploy**
   ```bash
   # Manual deploy via Railway CLI
   npm install -g @railway/cli
   railway link
   railway up
   
   # Or via GitHub - auto deploy on push to main
   ```

## Monitoring & Logs

```bash
# View logs via Railway CLI
railway logs

# View logs via Railway Dashboard
# https://railway.app/dashboard
```

## Health Checks

The application includes health check endpoints:
- `GET /health` - Basic health check
- `GET /metrics` - Prometheus metrics (if enabled)

## Rollback

```bash
# Rollback to previous deployment
railway rollback
```

## CI/CD Pipeline Status

Once `.github/workflows/ci-cd.yml` is created, the following will happen automatically:

- ✅ Lint on every push
- ✅ Run tests on every push
- ✅ Build Docker image on main/develop
- ✅ Push to GitHub Container Registry
- ✅ Deploy to Railway on main branch push
- ✅ Security scanning with Trivy

## Troubleshooting

### Build Fails
- Check `npm run build` locally
- Verify Node version (18.x)
- Check for missing dependencies

### Deploy Fails
- Verify environment variables are set
- Check database connectivity
- View Railway logs

### Port Issues
- Ensure PORT is set to 3000
- Check Railway port configuration

## Support

For issues with Railway deployment, visit:
https://docs.railway.app
