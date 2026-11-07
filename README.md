# d2r-mobile build workflow

[English](README.md) | [简体中文](README.zh-CN.md)

Build iOS and macOS apps from [d2r-mobile](https://github.com/jhaizhou-ops/d2r-mobile) source with GitHub Actions. Each run defaults to the latest official upstream Release and publishes to your private repository.

## Configure and build

1. Click [Use this template](https://github.com/jiayx/d2r-mobile-build/generate) and create a **Private** repository.
2. In **Actions**, select **Build IPA** (iOS) or **Build macOS**, click **Run workflow**, and paste the JSON for your platform into **`prepared_input`**:

   **Build IPA (iOS)**

   ```json
   {
     "url": "https://ipfs.filebase.io/ipns/k51qzi5uqu5dkbfnqcjbd6jlgbckojtl4gu7m1kgu8esex1zg4oo485o5cjop2/D2RMobile-Prepared.zip",
     "sha256_url": "https://ipfs.filebase.io/ipns/k51qzi5uqu5dkbfnqcjbd6jlgbckojtl4gu7m1kgu8esex1zg4oo485o5cjop2/Prepared-SHA256SUMS.txt"
   }
   ```

   **Build macOS**

   ```json
   {
     "url": "https://ipfs.filebase.io/ipns/k51qzi5uqu5dkbfnqcjbd6jlgbckojtl4gu7m1kgu8esex1zg4oo485o5cjop2/D2RMobile-MacPrepared.zip",
     "sha256_url": "https://ipfs.filebase.io/ipns/k51qzi5uqu5dkbfnqcjbd6jlgbckojtl4gu7m1kgu8esex1zg4oo485o5cjop2/MacPrepared-SHA256SUMS.txt"
   }
   ```

   The Filebase IPNS URLs are stable; package updates keep these addresses and refresh their checksum files.

   The prepared packages are approximately **287 MB for iOS** and **292 MB for macOS**.

3. Click **Run workflow** to start the build. Downloading, compiling, packaging and publishing typically takes **about 6 minutes for iOS** or **7 minutes for macOS**.

- Run with the defaults to compile the latest official upstream Release.
- To test development code, set `source_ref` to `main`, another branch, a tag, or a commit.
- To test your changes, set `source_repository` to your fork and `source_ref` to its branch. For private source repositories, add a **`SOURCE_TOKEN`** Secret with Contents read access to that repository.

The build entry automatically uses this project's latest build logic. Repeated builds and reruns of the same upstream version each receive independent Release and file names.

To prepare your own inputs, see [Generate an iOS prepared package](docs/PREPARED_INPUT.md#generate-an-ios-prepared-package) or [Generate a macOS prepared package](docs/MACOS_PREPARED_INPUT.md#generate-a-macos-prepared-package).

## Download and use on iOS

After the build, download from your repository’s **Releases**:

| File | Purpose |
|---|---|
| `D2RMobile-<version>-build.<run>.<attempt>.ipa` | iOS 26 and later |
| `D2RMobile-<version>-build.<run>.<attempt>-ios18.ipa` | iOS 18–25 |
| `SHA256SUMS.txt`, `build-report.json` | Checksums and build details |

Download the community-provided [game resources (Data and Legacy)](https://drive.google.com/drive/folders/1lfjUghi54ohyDxYEtNuEjtGUZyGovaIA):

| Package | Download size | Purpose |
|---|---|---|
| `D2R-Mobile-Resources.zip.001`, `.002`, `.003` | 5.42 GB total | Data required on every supported device; contains the `D2R Mobile Resources` folder with 18 `.data` files |
