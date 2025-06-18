# Kids Ubuntu VM Setup

A complete Ubuntu virtual machine configuration designed for children, featuring dedicated GPU passthrough for gaming, educational software, and streamlined access to streaming services. Perfect for providing kids with a safe, controlled computing environment for schoolwork, entertainment, and learning.

## Features

### 🖥️ **Complete VM Environment**
- Ubuntu desktop optimized for children
- Dedicated GPU passthrough for gaming performance
- Isolated environment for safety and control

### 🎬 **Integrated Streaming Access**
- Dedicated Netflix and Disney+ launcher icons
- Fullscreen kiosk mode for distraction-free viewing
- Simple Alt+F4 exit to return to desktop
- No complex browser navigation required

### 🎮 **Gaming Ready**
- GPU passthrough configuration for modern games
- Performance optimized for child-appropriate gaming
- Seamless integration with educational and entertainment software

### 📚 **Education Friendly**
- Suitable for schoolwork and educational applications
- Clean, organized desktop environment
- Easy-to-use interface for children

## What's Included

### Configuration Files
- `vm-config.xml` - Complete VM configuration with GPU passthrough
- `netflix-app.desktop` - Netflix launcher application
- `disneyplus-app.desktop` - Disney+ launcher application
- `setup-streaming.sh` - Automated streaming setup script
- `install-essentials.sh` - Essential software installation script

### Resources
- Netflix and Disney+ icon files
- Documentation and setup guides
- Troubleshooting tips

## Hardware Requirements

### Host System
- Modern CPU with virtualization support (Intel VT-x/AMD-V)
- Minimum 16GB RAM (32GB recommended)
- Two graphics cards OR one GPU + integrated graphics
- Adequate storage (500GB+ recommended)

### VM Allocation
- 8GB+ RAM allocated to VM
- 4+ CPU cores
- Dedicated GPU passed through
- 100GB+ storage space

## Software Requirements

### Host System
- Linux host with KVM/QEMU support
- VFIO modules configured
- GPU passthrough capability

### Guest System (VM)
- Ubuntu 20.04+ or similar distribution
- Chromium browser for streaming
- Gaming-compatible drivers

## Quick Setup Guide

### 1. VM Configuration

Import the provided VM configuration:
```bash
# Import VM configuration
virsh define vm-config.xml

# Start the VM
virsh start kids-ubuntu-vm
```

### 2. Install Base System

Boot Ubuntu and complete initial setup:
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install essential packages
sudo apt install chromium-browser ubuntu-restricted-extras
```

### 3. Setup Streaming Apps

Run the automated setup:
```bash
# Make setup script executable
chmod +x setup-streaming.sh

# Run setup
./setup-streaming.sh
```

Or manually create the streaming launchers:

**Netflix App:**
```bash
cat > ~/.local/share/applications/netflix-app.desktop << 'EOF'
[Desktop Entry]
Name=Netflix
Comment=Netflix Streaming
Exec=chromium-browser --app=https://netflix.com --start-maximized
Icon=netflix
Type=Application
Categories=AudioVideo;Network;
StartupNotify=true
StartupWMClass=netflix.com
EOF
```

**Disney+ App:**
```bash
cat > ~/.local/share/applications/disneyplus-app.desktop << 'EOF'
[Desktop Entry]
Name=Disney+
Comment=Disney Plus Streaming
Exec=chromium-browser --kiosk https://disneyplus.com
Icon=disneyplus
Type=Application
Categories=AudioVideo;Network;
StartupNotify=true
EOF
```

### 4. Install Icons

```bash
# Create icons directory
mkdir -p ~/.local/share/icons

# Copy streaming service icons
cp netflix-icon.png ~/.local/share/icons/netflix.png
cp disney-icon.png ~/.local/share/icons/disneyplus.png

# Update desktop database
update-desktop-database ~/.local/share/applications/
```

### 5. Add to Panel

1. Press **Super** key
2. Search for "Netflix" and "Disney+"
3. Right-click each app → "Add to Favorites"
4. Icons will appear in the dock alongside games and other apps

## Usage Instructions

### For Kids
- **Netflix**: Click the red Netflix icon to watch shows and movies
- **Disney+**: Click the blue Disney+ icon to watch Disney content
- **Exit**: Press **Alt + F4** together to go back to desktop
- **Switch Apps**: Press the **Super** key (Windows logo) to see all apps

### For Parents/Admins
- VM can be paused/resumed as needed
- Snapshots can be taken for easy restore points
- Network access can be controlled at host level
- GPU can be reclaimed by host when VM is shut down

## Gaming Setup

The VM includes GPU passthrough for gaming performance:

1. **Install Steam**: Available in Ubuntu Software Center
2. **Install Gaming Drivers**: NVIDIA/AMD drivers included
3. **Configure Controllers**: USB passthrough for gaming controllers
4. **Performance**: Near-native gaming performance with dedicated GPU

## Educational Software

Recommended educational applications:
- **LibreOffice**: For documents and presentations
- **GIMP**: Image editing and creativity
- **Scratch**: Programming education for kids
- **Educational Games**: Available through Ubuntu repositories

## Security and Safety

### Built-in Protections
- Isolated VM environment prevents host system access
- Streaming apps launch directly to content (no web browsing)
- Parental controls can be implemented at network level
- VM can be easily reset to clean state

### Optional Enhancements
- Install parental control software (Qustodio, etc.)
- Configure DNS filtering at router level
- Set up time-based access controls
- Enable automatic backups/snapshots

## Troubleshooting

### Streaming Issues
- **Black screen**: Check GPU passthrough configuration
- **No video playback**: Install `chromium-codecs-ffmpeg-extra`
- **Login problems**: Clear browser data in Chromium
- **Audio issues**: Verify PulseAudio configuration

### Performance Issues
- **Slow graphics**: Verify GPU passthrough is working
- **Lag**: Check RAM allocation (increase if needed)
- **Stuttering**: Ensure CPU pinning is configured properly

### VM Issues
- **Won't start**: Check VFIO modules and IOMMU groups
- **No display**: Verify GPU assignment and monitor connection
- **Input lag**: Check USB controller passthrough

## Customization

### Adding More Streaming Services
Create additional `.desktop` files for other services:
```bash
cat > ~/.local/share/applications/service-name.desktop << 'EOF'
[Desktop Entry]
Name=Service Name
Exec=chromium-browser --kiosk https://service-url.com
Icon=service-icon
Type=Application
Categories=AudioVideo;Network;
EOF
```

### Gaming Enhancements
- Install additional game stores (Lutris, Heroic Launcher)
- Configure game-specific optimizations
- Set up game controller mappings

### Educational Customization
- Install subject-specific educational software
- Configure kid-friendly bookmarks
- Set up homework/project directories

## Support and Contributing

### Getting Help
- Check the troubleshooting section above
- Review VM logs: `journalctl -u libvirtd`
- Verify hardware compatibility

### Contributing
- Report issues with specific error messages
- Share additional educational software recommendations
- Submit improvements to VM configuration
- Add support for additional streaming services

## License

This configuration is provided as-is for educational and personal use. Streaming service access requires valid subscriptions. Gaming performance depends on hardware configuration.

---

**Note**: This setup requires technical knowledge of virtualization and GPU passthrough. Ensure you understand the implications of GPU passthrough before implementing in production environments.
