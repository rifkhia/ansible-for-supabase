# Ansible for Supabase

An Ansible playbook for deploying and managing Supabase infrastructure using Docker containers. This automation handles the complete Supabase stack including PostgreSQL, authentication, real-time features, storage, and analytics.

## 🚀 Features

- **Complete Supabase Stack**: Deploy all core Supabase services
- **Docker-based**: Containerized deployment for consistency and portability
- **Configuration Management**: Template-based configuration with environment-specific variables
- **Service Discovery**: Automated service networking and dependencies
- **SSL/TLS Support**: Kong gateway with SSL termination
- **Monitoring & Logging**: Vector-based log aggregation and analytics
- **Database Management**: Automated PostgreSQL setup with extensions and migrations

## 📋 Prerequisites

- **Ansible** >= 2.9
- **Docker** and **Docker Compose** on target hosts

## 📁 Project Structure

```
├── inventory                          
│   └── dev
│       ├── host_vars
│       │   └── supa_1.yml
│       └── hosts.yml
├── templates
│   ├── db
│   │   ├── _supabase.sql
│   │   ├── init
│   │   │   └── data.sql
│   │   ├── jwt.sql
│   │   ├── logs.sql
│   │   ├── pooler.sql
│   │   ├── realtime.sql
│   │   ├── roles.sql
│   │   └── webhooks.sql
│   ├── functions
│   │   ├── hello
│   │   │   └── index.ts
│   │   └── main
│   │       └── index.ts
│   ├── kong
│   │   └── kong.yml.j2
│   ├── logs
│   │   └── vector.yml.j2
│   └── pooler
│       └── pooler.exs
├── deploy_service.yml
├── main.yml
├── precheck.yaml
├── prepare_configs.yml
└── readme.md

```

## 🚀 Deployment

### Quick Start

1. **Clone the repository**:
   ```bash
   git clone https://github.com/rifkhia/ansible-for-supabase.git
   cd ansible-for-supabase
   ```

2. **Configure your inventory**:
   ```bash
   vim inventory/dev/hosts.yml
   #Edit inventory/hosts with your server details
   ```

3. **Set your variables**:
   ```bash
   vim inventory/host_vars/supa_1.yml
   # Edit inventory/group_vars/all.yml with your configuration
   ```

4. **Deploy Supabase**:
   ```bash
   ansible-playbook -i inventory/dev deploy.yml
   ```
   
## ⚙️ Configuration
### Variables Configuration

Configure your deployment in `inventory/dev/supa_1.yml`:

```yaml
# Basic Configuration
base_dir:  # Base directory for supabase
config_path:  # Where config stored
docker_network:  # Docker network name

supabase_tenant_id:  # Supabase supavisor tenant (connection pool)
supabase_studio_organization:  # Supabase studio organization name
supabase_studio_project:  # Supabase studio project name

docker_socket_path: 

kong_http_port:  # Kong http port
kong_https_port:  # Kong https port

# Database Configuration
postgres:
  host: "postgres"
  port: 5432
  db: "postgres"
  password: "your-secure-password"
  
# Authentication
supabase_dashboard_username:  # Supabase dashboard username login credentials
supabase_dashboard_password:  # Supabase dashboard password login credentials
supabase_anon_key:  # JWT Token as Anonymous
supabase_service_role_key:  # JWT Token as Service Role (Bypass RLS)
supabase_jwt_secret:  # JWT Secret for generating token
supabase_jwt_expiry:  # JWT Expired time token

# SMTP Configuration
smtp: 
  email: 
  host: 
  port: 
  user: 
  password: 
  name: 


# Service configuration
services:

```

## 🔧 Customization

### Adding Custom Database Scripts

Place your SQL scripts in the appropriate template directories:

- **Migrations**: `templates/db/`
- **Initialization**: `templates/db/init/`

### Custom Edge Functions

Add your TypeScript functions to:
```
templates/functions/your-function/index.ts
```

### Kong Configuration

Modify the Kong gateway settings in:
```
templates/kong/kong.yml.j2
```

## 🔍 Monitoring & Logs

### Analytics Dashboard

Access the Logflare analytics dashboard at:
```
https://your-domain.com:4000
```

## 🔒 Security Considerations

- **Change default passwords** in production
- **Use strong JWT secrets** (minimum 32 characters)
- **Enable SSL/TLS** for production deployments
- **Configure firewall rules** to restrict access
- **Regular security updates** for base images
- **Monitor access logs** regularly

## To Do
- Support external database
- More flexibility for removing one of service

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

**⭐ Star this repository if it helped you deploy Supabase with Ansible!**