# n8n-Tailscale

A portable, self-hosted n8n instance with Tailscale Funnel access.

## Features
- **Tailscale Sidecar**: Securely connect your n8n instance to your tailnet.
- **Funnel Access**: Access your n8n instance via `https://n8n.<your-tailnet>.ts.net`.
- **Local Access**: Accessible at `http://localhost:5678`.
- **Persistence**: Data and Tailscale state are persisted across restarts.

## Prerequisites
- Tailscale account.
- Tailscale Auth Key (Reusable recommended).
- Docker and Docker Compose installed.

## Setup Instructions

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd n8n-tailscale
   ```

2. **Configure environment variables**:
   Copy `.env.example` to `.env` and fill in the values.
   ```bash
   cp .env.example .env
   ```
   - `TS_AUTHKEY`: Your Tailscale Auth Key.
   - `N8N_ENCRYPTION_KEY`: A unique string for encryption. You can generate one using:
     ```bash
     openssl rand -hex 32
     ```

3. **Start the stack**:
   ```bash
   docker compose up -d
   ```

5. **Access n8n**:
   - Local: [http://localhost:5678](http://localhost:5678)
   - Public: `https://n8n.<your-tailnet>.ts.net`

## Architecture

The project uses a sidecar pattern where the `n8n` container shares the network namespace of the `tailscale` container. This allows Tailscale to manage all networking, including SSL termination and proxying for the Funnel.

