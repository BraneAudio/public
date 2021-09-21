# bluez_v5.55_do-not-enable-pairing-on-agent-register.patch
Commit 1880b299086659844889cdaf687133aca5eaf102 added code that would enable
pairing when an agent registered.  This patch disables this code block.

# bluez_v5.55_fix-error-in-set_mode.patch
The set_mode function in adapter.c appears to have several errors that are
addressed in this patch.  The changes ought to be self explanatory.

# Build
Patches include the blues release in their name.  Currently the same config is
used for all versions of bluez.  Configure bluez with the following args:

./configure \
   --enable-test \
   --enable-datafiles \
   --enable-library \
   --without-zsh-completion-dir \
   --enable-debug \
   --disable-static \
   --enable-shared \
   --enable-a2dp \
   --enable-avrcp \
   --disable-btpclient \
   --disable-cups \
   --enable-deprecated \
   --disable-health \
   --enable-hid \
   --enable-hog \
   --disable-mesh \
   --disable-midi \
   --enable-network \
   --disable-nfc \
   --enable-obex \
   --enable-client \
   --disable-sap \
   --disable-sixaxis \
   --enable-systemd \
   --enable-testing \
   --enable-threads \
   --enable-tools \
   --enable-udev \
   --host=armv7l
