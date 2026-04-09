# Instructions on how to create a flatpak version of LocalPDF Studio.

## 1. Clone this repository
```bash
git clone https://github.com/Alinur1/LocalPDF_Studio_Flatpak.git
```

## 2. Install flatpak-builder if you don't have it
```bash
sudo apt install flatpak-builder
```
```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
```bash
flatpak install flathub org.freedesktop.Platform//25.08 org.freedesktop.Sdk//25.08
```
```bash
flatpak install flathub org.electronjs.Electron2.BaseApp//25.08
```

## 3. Build and install locally
```bash
flatpak-builder --user --install --force-clean build-dir \
  io.github.alinur1.LocalPDF_Studio.yml
```

## 4. Run it
```bash
flatpak run io.github.alinur1.LocalPDF_Studio
```

## 5. To remove/uninstall it
```bash
flatpak remove io.github.alinur1.LocalPDF_Studio
```

# Linter: (not necessary actually)
## 6. First install the builder
```bash
flatpak install flathub org.flatpak.Builder
```

## 7. Run linter for the metainfo file
```bash
flatpak run --command=flatpak-builder-lint org.flatpak.Builder appstream io.github.alinur1.LocalPDF_Studio.metainfo.xml
```

## 8. Run linter for the manifest file
```bash
flatpak run --command=flatpak-builder-lint org.flatpak.Builder manifest io.github.alinur1.LocalPDF_Studio.yml
```

### That's it. Now you can use LocalPDF Studio as flatpak in your device. Please note that, by following this process, you will not receive any updates automatically. You have to follow the steps again to get the latest update.