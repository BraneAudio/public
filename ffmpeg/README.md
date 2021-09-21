# ffmpeg_v4.2.2_expanded-http-header-support.patch
Added for avs audio player v1.5; supports adding separate custon http headers
for fetching manifests, decryption keys, and audio segments.  DOES NOT include
patching for the sample-aes support in a previous patch but is easily added.

# ffmpeg_v4.2.2_mma-ignore-http-416.patch
Ignore http 416 under specific conditions to avoid a problem with aac-lc audio
served by media monkey android.

# ffmpeg_v4.2.2_mma-mp3dec-error-handling.patch
Changed a uint64_t to an int64_t for error return value parsing.  Fixed an error
rendering mp3 audio from media monkey android.

# ffmpeg_v4.2.1_cache-redirect.patch
It is possible to get hls playlists whose contents are redirected.  When this
happens ffmpeg is closing and opening at least two urls every segment duration.
This can make the stream stutter and fail due to the extra overhead.  This patch
modifies ffmpeg to cache one redirect connection which it will use as needed.

# ffmpeg_v4.2.1_sample-aes.patch
This patch adds support for sample-aes encrypted hls streams.  Audio and video
streams are supported but only audio streams have been tested.

# Build
Patches include the ffmpeg release in their name.  Currently the same config is
used for all versions of ffmpeg.  Configure ffmpeg with the following args:

./configure \
--disable-stripping \
--enable-pic \
--enable-shared \
--enable-pthreads \
--sysroot=/opt/sysroots/cortexa7hf-neon-poky-linux-gnueabi/ \
--cross-prefix=arm-poky-linux-gnueabi- \
--ld='arm-poky-linux-gnueabi-gcc -mfpu=neon -mfloat-abi=hard -mcpu=cortex-a7' \
--cc='arm-poky-linux-gnueabi-gcc -mfpu=neon -mfloat-abi=hard -mcpu=cortex-a7' \
--cxx='arm-poky-linux-gnueabi-g++ -mfpu=neon -mfloat-abi=hard -mcpu=cortex-a7' \
--arch=arm \
--target-os=linux \
--enable-cross-compile \
--extra-cflags=' -O2 -pipe -g -feliminate-unused-debug-types' \
--extra-ldflags='-Wl,-O1 -Wl,--hash-style=gnu -Wl,--as-needed' \
--libdir=/usr/lib \
--shlibdir=/usr/lib \
--datadir=/usr/share/ffmpeg \
--disable-mipsdsp \
--disable-mipsdspr2 \
--cpu=cortex-a7 \
--pkg-config=pkg-config \
--enable-alsa \
--enable-avcodec \
--enable-avdevice \
--enable-avfilter \
--enable-avformat \
--enable-avresample \
--enable-bzlib \
--enable-gnutls \
--disable-gpl \
--disable-libgsm \
--disable-indev=jack \
--enable-libvorbis \
--enable-lzma \
--disable-libmfx \
--disable-libmp3lame \
--disable-openssl \
--enable-libopus \
--enable-postproc \
--disable-sdl2 \
--disable-libspeex \
--enable-swresample \
--enable-swscale \
--disable-libtheora \
--disable-vaapi \
--disable-vdpau \
--disable-libvpx \
--disable-libx264 \
--disable-libxcb \
--disable-outdev=xv \
--enable-zlib \
--disable-static \
--disable-programs \
--disable-doc
