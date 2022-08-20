TESTED ON Galaxy Tab S7 (rooted) with Fedora 36 via termux
```bash
sudo dnf install scons pkgconfig libX11-devel libXcursor-devel libXrandr-devel libXinerama-devel libXi-devel mesa-libGL-devel mesa-libGLU-devel alsa-lib-devel pulseaudio-libs-devel libudev-devel gcc-c++ libstdc++-static libatomic-static
```
*if the above doesn't work, some packages from the 'archived' stuff below might be needed*
~~Clone this repo~~
```bash
#git clone https://github.com/akien-mga/godot
```
Download the release instead:
```bash
curl -OL https://github.com/akien-mga/godot/releases/tag/3.5-stable
```
```bash
cd godot
```
```bash
scons platform=x11 tools=yes target=release_debug
```
-----
IGNORE BELOW, SAVED FOR ARCHIVAL REASONS (might need it for compiling other stuff)
### Building using .spec file, then scons
```bash
sudo yum install rpm-build fedora-packager freetype-devel GLC_lib-devel python3-scons alsa-lib-devel bullet-devel rust-libpulse-binding-devel rust-libudev-devel libwebp-devel libzstd-devel libogg-devel opus-devel opusfile-devel libtheora-devel libvorbis-devel libvpx-devel desktop-file-utils embree-devel mbedtls-devel miniupnpc-devel 
```
```bash
rpmdev-setuptree
```
```bash
curl -Lo ~/rpmbuild/SOURCES/godot-3.5-stable.tar.xz https://downloads.tuxfamily.org/godotengine/3.5/godot-3.5-stable.tar.xz
```
```bash
curl -Lo ~/rpmbuild/SOURCES/godot-3.5-stable.tar.xz.sha256 https://downloads.tuxfamily.org/godotengine/3.5/godot-3.5-stable.tar.xz.sha256
```
```bash
git clone https://src.fedoraproject.org/rpms/godot.git
```
```bash
rpmbuild -ba godot.spec
```
```bash
cd ~/rpmbuild/BUILD/godot-3.5-stable/
```
```bash
scons platform=x11 tools=yes target=release_debug
```
 Termux seems to crash before the last step completes, which prevents it from finishing
----