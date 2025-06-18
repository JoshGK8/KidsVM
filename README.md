# KidsVM

Ubuntu virtual machine with GPU passthrough for gaming, streaming, and education. A safe, controlled environment for kids' computing.

## Features
- 🖥️ Ubuntu desktop with GPU passthrough for gaming
- 🎬 Netflix & Disney+ kiosk launchers
- 🎮 Native gaming performance
- 📚 Education-ready environment

## Files Included
- `KidsVM.xml` - VM configuration with GPU passthrough
- `netflix-app.desktop` - Netflix launcher
- `disneyplus-app.desktop` - Disney+ launcher

## Requirements
- **Host**: 16GB+ RAM, 2 GPUs (or 1 GPU + integrated), KVM/QEMU with VFIO
- **VM**: 10GB RAM, 6 CPUs, GPU passthrough, 100GB+ storage

## Quick Setup

### 1. Import VM
```bash
virsh define KidsVM.xml
virsh start KidsVM
```

### 2. In VM: Install streaming apps
```bash
# Copy desktop files to applications folder
cp *.desktop ~/.local/share/applications/

# Update desktop database
update-desktop-database ~/.local/share/applications/
```

### 3. Add to dock
- Press Super key, search for "Netflix" or "Disney+"
- Right-click → "Add to Favorites"

## Usage
- **Kids**: Click Netflix/Disney+ icons, press Alt+F4 to exit
- **Parents**: VM snapshots, network controls, pause/resume anytime

## Key Features
- **Gaming**: Native GPU performance via passthrough
- **Safety**: Isolated VM environment, kiosk mode streaming
- **Education**: Full Ubuntu desktop for schoolwork

## Troubleshooting
- **No video**: Install `chromium-codecs-ffmpeg-extra`
- **GPU issues**: Check VFIO modules and IOMMU groups
- **VM won't start**: Verify GPU assignment in KidsVM.xml

## Notes
- GPU passthrough requires IOMMU enabled in BIOS
- Streaming services require valid subscriptions
- VM paths in XML may need adjustment for your system
