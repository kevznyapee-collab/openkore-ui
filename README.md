# OpenKore Bot Manager UI

A lightweight, high-performance desktop application for managing multiple OpenKore bot accounts with real-time status monitoring.

## Features

- 🎮 **Multi-Account Management** - Handle unlimited bot accounts
- ⚡ **Ultra-Lightweight** - ~15MB footprint, minimal CPU/RAM usage
- 📊 **Real-Time Status** - Monitor HP, SP, EXP, Zeny, Location
- 🎮 **Easy Controls** - Start/Stop/Pause per account
- 🗺️ **Map Viewer** - Visual map display (ready for integration)
- 🔗 **OpenKore Integration** - Direct communication with OpenKore
- 💾 **Persistent Storage** - Account configs auto-saved
- 🌍 **Cross-Platform** - Windows, macOS, Linux

## Tech Stack

- **Frontend**: React 18 + TypeScript + Tailwind CSS
- **Desktop**: Tauri (ultra-lightweight native wrapper)
- **State**: Zustand (minimal state management)
- **Backend**: Rust + Tokio (async runtime)

## Quick Start

### Prerequisites
- Node.js 16+
- Rust 1.70+
- OpenKore installed and running

### Installation

```bash
# Clone repository
git clone https://github.com/kevznyapee-collab/openkore-ui
cd openkore-ui

# Install dependencies
npm install

# Install Rust (if not already)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### Development

```bash
# Start dev server with hot reload
npm run dev
```

This opens the app window and enables live reloading as you make changes.

### Production Build

```bash
# Build for your platform
npm run build

# Output: ./src-tauri/target/release/openkore-ui
```

## OpenKore Integration

See [OPENKORE_INTEGRATION.md](./OPENKORE_INTEGRATION.md) for detailed setup instructions.

### Quick Setup

1. Copy `status_server.pl` to `control/modules/` in your OpenKore directory
2. Add this line to `control/config.txt`:
   ```
   module Modules/status_server.pl
   ```
3. Restart OpenKore
4. Start the UI - it will auto-connect to OpenKore

## Project Structure

```
openkore-ui/
├── src/
│   ├── components/          # React components
│   │   ├── AccountList.tsx
│   │   ├── AccountSlot.tsx
│   │   ├── StatusDisplay.tsx
│   │   ├── MapViewer.tsx
│   │   ├── MainPanel.tsx
│   │   └── AddAccountModal.tsx
│   ├── store/              # Zustand state management
│   ├── services/           # API service layer
│   ├── types/              # TypeScript interfaces
│   ├── App.tsx
│   └── main.tsx
├── src-tauri/
│   ├── src/               # Rust backend
│   ├── tauri.conf.json    # Tauri configuration
│   └── Cargo.toml
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
└── tailwind.config.js
```

## Commands

### Available NPM Scripts

```bash
npm run dev           # Development with hot reload
npm run build         # Production build
npm run preview       # Preview production build
npm run type-check    # TypeScript validation
npm run lint          # ESLint check
npm run format        # Prettier formatting
```

## API Reference

### Account Management

```typescript
// Add account
await apiService.addAccount(account);

// Remove account
await apiService.removeAccount(accountId);

// Get all accounts
const accounts = await apiService.getAccounts();
```

### Bot Control

```typescript
// Start bot
await apiService.startBot(accountId);

// Stop bot
await apiService.stopBot(accountId);

// Pause bot
await apiService.pauseBot(accountId);

// Resume bot
await apiService.resumeBot(accountId);
```

### Status Monitoring

```typescript
// Get single bot status
const status = await apiService.getBotStatus(accountId);

// Get all statuses
const allStatus = await apiService.getAllStatus();
```

## Performance

- **Memory**: ~80-150MB (single instance)
- **CPU**: 1-3% at idle, 5-10% with active bots
- **Startup Time**: ~2-3 seconds
- **Status Update**: 100-500ms per account

## Troubleshooting

### App won't start
- Ensure OpenKore is running
- Check OpenKore is listening on port 6969
- View logs in DevTools (Ctrl+Shift+I)

### Status not updating
- Verify `status_server.pl` is loaded in OpenKore
- Check OpenKore console for errors
- Restart both OpenKore and the UI

### High CPU usage
- Reduce refresh interval in settings
- Close unnecessary accounts
- Check for OpenKore memory leaks

## Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## License

MIT License - see [LICENSE](./LICENSE) file

## Support

For issues and questions:
- GitHub Issues: [Report a bug](https://github.com/kevznyapee-collab/openkore-ui/issues)
- Discussions: [Ask a question](https://github.com/kevznyapee-collab/openkore-ui/discussions)
