# Docker CalDAV Server Setup

This setup uses Radicale as a lightweight CalDAV server that can be easily deployed using Docker.

## Prerequisites

- Docker
- Docker Compose

## Environment Variables

### Deployment Configuration
- `DEPLOYMENT_TYPE`: Set to 'local' for LAN/HTTP or 'public' for WAN/HTTPS deployment
- `HOSTNAME`: Your server's hostname or domain name (required for public deployment)
- `ALLOWED_IPS`: Comma-separated list of IPv4 addresses/ranges allowed to access the calendar

### Calendar Instance Configuration
- `CALENDAR_NAME`: Unique name for this calendar instance
- `CALENDAR_USERNAME`: Username for calendar access
- `CALENDAR_PASSWORD`: Password for calendar access
- `CALENDAR_PORT`: Port number for this calendar instance

### Calendar Access Configuration
- `ENABLE_PUBLIC_FULL`: Enable public read-only access to full calendar details
- `ENABLE_PUBLIC_FREEBUSY`: Enable public read-only access to free/busy information
- `ENABLE_PRIVATE_FULL`: Enable authenticated access to full calendar details
- `ENABLE_PRIVATE_FREEBUSY`: Enable authenticated access to free/busy information

### Let's Encrypt Configuration
- `LETSENCRYPT_TYPE`: 'test' for staging or 'prod' for production certificates
- `LETSENCRYPT_EMAIL`: Email address for Let's Encrypt notifications
- `LETSENCRYPT_AGREE_TOS`: Set to true to agree to Let's Encrypt Terms of Service

### Calendar Data Configuration
- `DATA_PATH`: Path to store calendar data
- `CONFIG_PATH`: Path to store configuration files
- `TIMEZONE`: Calendar timezone (e.g., UTC, America/New_York)

### Security
- `REGENERATE_PUBLIC_LINKS`: Set to true to regenerate public calendar links

## Setup Instructions

1. Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

2. Modify the `.env` file with your desired settings

3. Create the necessary directories:
   ```bash
   mkdir -p data/calendar1 config/calendar1
   ```

4. Start the server:
   ```bash
   docker-compose up -d
   ```

## Calendar URLs

### Public Access (if enabled)
- Full Calendar: `http(s)://your-server:port/public/calendar.ics`
- Free/Busy Only: `http(s)://your-server:port/public/freebusy.ics`

### Authenticated Access
- Full Calendar: `http(s)://your-server:port/calendar/user/calendar.ics`
- Free/Busy Only: `http(s)://your-server:port/calendar/user/freebusy.ics`

## Multiple Calendars

To run multiple calendar instances:
1. Uncomment and modify the second section in the `.env` file
2. Create additional data and config directories
3. Each instance will have its own port and configuration

## Security Notes

- Use HTTPS (public deployment) for production environments
- Regularly change passwords
- Use strong passwords
- Restrict IP access using `ALLOWED_IPS` for additional security
- Public calendar links can be regenerated by setting `REGENERATE_PUBLIC_LINKS=true`
- Monitor Let's Encrypt certificate renewals
- Keep Docker and all components updated