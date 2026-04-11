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

## 3. Generate "generated-sources.json" file using python (don't forget to use virtual environment)
```bash
python3 -m venv flatpak-tools-env
```
```bash
source flatpak-tools-env/bin/activate
```
Note: v3.0.0 is a release tag of LocaLPDF Studio. Change the tag when a new version releases. Check here for new release and it's tag number: https://github.com/Alinur1/LocalPDF_Studio/releases 
```bash
wget https://raw.githubusercontent.com/Alinur1/LocalPDF_Studio/refs/tags/v3.0.0/package-lock.json
```
```bash
pip install git+https://github.com/flatpak/flatpak-builder-tools.git#subdirectory=node
```
```bash
flatpak-node-generator npm package-lock.json -o generated-sources.json
```
```bash
rm package-lock.json
```
```bash
deactivate
```

## 4. Build and install locally
```bash
flatpak-builder --user --install --force-clean build-dir \
  io.github.alinur1.LocalPDF_Studio.yml
```

## 5. Run it
```bash
flatpak run io.github.alinur1.LocalPDF_Studio
```

## 6. To remove/uninstall it
```bash
flatpak remove io.github.alinur1.LocalPDF_Studio
```

# Linter: (not necessary actually)
## 7. First install the builder
```bash
flatpak install flathub org.flatpak.Builder
```

## 8. Run linter for the metainfo file
```bash
flatpak run --command=flatpak-builder-lint org.flatpak.Builder appstream io.github.alinur1.LocalPDF_Studio.metainfo.xml
```

## 9. Run linter for the manifest file
```bash
flatpak run --command=flatpak-builder-lint org.flatpak.Builder manifest io.github.alinur1.LocalPDF_Studio.yml
```

### That's it. Now you can use LocalPDF Studio as flatpak in your device. Please note that, by following this process, you will not receive any updates automatically. You have to follow the steps again to get the latest update.