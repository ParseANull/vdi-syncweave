# SyncWeave Vagrant Build Steps (VirtualBox, no WSL)

This path gives us a Linux build environment without WSL by using Vagrant + VirtualBox.

## 1. Install VirtualBox on Windows

If VirtualBox is not installed, install it first:

```powershell
winget install Oracle.VirtualBox
```

Then close and reopen your terminal so PATH updates are visible.

Verify:

```powershell
VBoxManage --version
vagrant --version
```

## 2. Start the VM and provision tools

From the repository root:

```powershell
vagrant up
```

Provisioning installs:

- OpenJDK 21
- Ant 1.10.17 at /opt/apache-ant-1.10.17
- libxslt runtime and helper packages

The build helper also copies `tools/tmsxml_to_properties` to `/tmp` inside the VM
before running Ant, so Linux helper binaries are executable even when `/vagrant`
is mounted with restricted execute semantics.

## 3. Run the build in the VM

```powershell
vagrant ssh -c "bash /vagrant/build/scripts/build-in-vagrant.sh"
```

This script runs:

- `ant -f build.xml resolve`
- `ant -f build.xml rename_jars`
- `ant -f build.xml package`

## 4. Segmented builds to reduce cycle time

For iterative development, run narrower targets instead of full `package`.

Warm dependencies once per VM session:

```powershell
vagrant ssh -c "cd /vagrant && ant -f build.xml resolve rename_jars"
```

Build all connectors only:

```powershell
vagrant ssh -c "cd /vagrant && ant -f build.xml connectors-all"
```

Build all functions only:

```powershell
vagrant ssh -c "cd /vagrant && ant -f build.xml functions-all"
```

Build all parsers only:

```powershell
vagrant ssh -c "cd /vagrant && ant -f build.xml parsers-all"
```

Build only changed components (fastest loop):

```powershell
vagrant ssh -c "cd /vagrant && ant -f build.xml connectors/JDBCConnector connectors/LDAPConnector"
```

Before opening or updating a PR, run a broader validation:

```powershell
vagrant ssh -c "cd /vagrant && ant -f build.xml JARS"
```

Then run full assembly only when needed:

```powershell
vagrant ssh -c "cd /vagrant && ant -f build.xml package"
```

## 5. Validate success

A successful run ends with:

```text
BUILD SUCCESSFUL
Build completed successfully.
```

## 6. Useful VM operations

```powershell
vagrant status
vagrant halt
vagrant destroy -f
vagrant provision
```

## Troubleshooting

- `VBoxManage not found`:
  - Reopen terminal after install.
  - Confirm `C:\Program Files\Oracle\VirtualBox` is on PATH.

- `vagrant up` provider errors:
  - Ensure VirtualBox version is recent and matches your CPU virtualization settings.

- Build fails after script updates:
  - Run `vagrant provision` again to refresh the toolchain.
