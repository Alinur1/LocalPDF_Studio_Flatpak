# A guide to make a flatpak of LocalPDF Studio 
## 1. Build the Electron app from the actual project repo (actually it's not necessary, because the tar.gz file will be fetched from the GitHub release automatically. So you can continue from step-4.)
```bash
npm install
```
```bash
npm run dist
```
OR (to create only the unpacked file)
```bash
npx electron-builder --dir --linux
```

## 2. Package the unpacked output into a tarball
```bash
tar -czf localpdf-studio-unpacked.tar.gz -C build/linux-unpacked .
```

## 3. Get the Ghostscript release URL and sha256 (paste it into the manifest)
```bash
https://github.com/ArtifexSoftware/ghostpdl-downloads/releases
```


## 4. Install flatpak-builder if you don't have it
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

## 5. Build and install locally to test
```bash
flatpak-builder --user --install --force-clean build-dir \
  io.github.alinur1.LocalPDF_Studio.yml
```

## 6. Run it
```bash
flatpak run io.github.alinur1.LocalPDF_Studio
```

## 7. To remove/uninstall it
```bash
flatpak remove io.github.alinur1.LocalPDF_Studio
```

# Linter:
## 8. First install the builder
```bash
flatpak install flathub org.flatpak.Builder
```

## 9. Lint the metainfo file
```bash
flatpak run --command=flatpak-builder-lint org.flatpak.Builder appstream io.github.alinur1.LocalPDF_Studio.metainfo.xml
```

## 10 .Lint the manifest file
```bash
flatpak run --command=flatpak-builder-lint org.flatpak.Builder manifest io.github.alinur1.LocalPDF_Studio.yml
```