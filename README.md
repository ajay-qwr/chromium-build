# Chromium Build for Wolvic WebXR

This repository contains a GitHub Actions workflow to automatically build Chromium AARs with WebXR support for the Wolvic browser on YVR headsets.

## 🚀 Quick Start

1. **Trigger the build**:
   - Go to the **Actions** tab in this GitHub repository
   - Select "Build Chromium for Wolvic YVR"
   - Click **Run workflow**
   - Wait 2-6 hours for the build to complete

2. **Download the artifacts**:
   - Once complete, click on the workflow run
   - Download `chromium-aars-wolvic-yvr.zip`
   - Extract to get AARs and assets

3. **Integrate with Wolvic**:
   ```powershell
   # Create directory for AARs
   mkdir C:\chromium_aar
   
   # Copy the AARs from extracted artifacts
   copy artifacts\aars\*.aar C:\chromium_aar\
   
   # Copy assets to Wolvic
   mkdir wolvic-main\app\src\chromium\assets
   copy artifacts\assets\* wolvic-main\app\src\chromium\assets\
   ```

4. **Configure Wolvic**:
   Add to `wolvic-main\local.properties`:
   ```ini
   chromium_aar=C:\\chromium_aar
   ```

5. **Build Wolvic with Chromium**:
   ```powershell
   cd wolvic-main
   .\gradlew assemblePfdmxrChromiumArm64Debug
   ```

## 📦 What Gets Built

- **Content.aar** - Chromium content library (~80MB)
- **ChromiumUi.aar** - Chromium UI library (~5MB)
- **Assets** - Runtime files (snapshot_blob, icudtl.dat, wolvic.pak)

## ⏱️ Build Time

- **Setup**: ~10 minutes
- **Source Download**: ~30 minutes
- **Compilation**: 2-4 hours
- **Total**: 2.5-5 hours

## 🎯 What This Enables

With these Chromium AARs, your Wolvic browser will support:
- ✅ Full WebXR immersive sessions
- ✅ Hand tracking in WebXR
- ✅ Passthrough/AR support
- ✅ All WebXR API features
- ✅ Native OpenXR performance

## 🔧 Technical Details

- **Target**: Android arm64-v8a (YVR headset)
- **Chromium Branch**: Igalia's wolvic-chromium (WebXR enabled)
- **Build Type**: Release (optimized for performance)
- **Runner**: Ubuntu 22.04 on GitHub Actions

## 📝 Notes

- The build runs on GitHub's servers (no local disk space needed)
- Artifacts are kept for 30 days
- You can re-run the workflow anytime to rebuild
- The workflow automatically handles M124 build issues

## 🐛 Troubleshooting

**Build times out after 6 hours**:
- This is the GitHub Actions limit for free accounts
- Try building locally instead (see Wolvic's CHROMIUM.md)

**Missing artifacts**:
- Check the workflow logs for errors
- Ensure the build completed successfully

**Wolvic won't build with Chromium**:
- Verify `chromium_aar` path in `local.properties`
- Check that assets are in `app/src/chromium/assets/`
- Select a "Chromium" build variant in Android Studio

## 📚 References

- [Wolvic Repository](https://github.com/Igalia/wolvic)
- [Wolvic Chromium Backend](https://github.com/Igalia/wolvic-chromium)
- [Chromium Build Instructions](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/android_build_instructions.md)

## 📄 License

This workflow is provided as-is for building Chromium with Wolvic modifications. Chromium and Wolvic have their own respective licenses.

