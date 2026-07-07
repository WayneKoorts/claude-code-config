# Skills Packages

This directory contains packaged skills (`.skill` files) that can be uploaded to Claude via the web interface at [claude.ai](https://claude.ai).

## Usage

1. Go to [claude.ai](https://claude.ai)
2. Enable the prerequisite: **Settings → Capabilities** → turn on "Code execution and file creation" (Team/Enterprise: **Organization settings → Skills**, enable both "Code execution and file creation" and "Skills")
3. Go to **Customize → Skills**, click **+**, choose **Create skill**, then **Upload a skill**, and upload the file to add the skill to your account

The packaged files here have a `.skill` extension but are plain ZIP archives. If the upload dialog only accepts `.zip`, rename the file's extension to `.zip` before uploading.

For more information on skills, see the [Claude Skills documentation](https://code.claude.com/docs/en/skills).

## Available Packages

| Package | Description |
|---------|-------------|
| `mdl2-icon-picker.skill` | Icon picker for Segoe MDL2 Assets (WinUI Windows apps) |
| `word-template-generator.skill` | Word document (.docx) generator using OOXML |
