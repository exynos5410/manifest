# HOW-TO Build

1) Initialize the repository

- repo init -u ssh://git@github.com/LineageOS/android.git -b cm-14.1

2) Add my manifest to the .repo folder (don't worry about the alert you will get about being DEPRECATED)

- cp local_manifest.xml .repo/

2) Sync latest LineageOS 14.1 sources

- repo sync -j20 --force-sync

3) Apply all Patches

- cd bootable/recovery-twrp
- git fetch https://gerrit.omnirom.org/android_bootable_recovery refs/changes/96/22096/3 && git cherry-pick FETCH_HEAD
- git fetch https://gerrit.omnirom.org/android_bootable_recovery refs/changes/68/22768/1 && git cherry-pick FETCH_HEAD
- git fetch https://gerrit.omnirom.org/android_bootable_recovery refs/changes/69/22769/1 && git cherry-pick FETCH_HEAD
- git fetch https://gerrit.omnirom.org/android_bootable_recovery refs/changes/70/22770/1 && git cherry-pick FETCH_HEAD
- cd ../..
- cd external/libselinux
- git am ../../device/samsung/i9500/patches/external_libselinux/556a9e925053e0b62f495233e165112e12b5d869.patch
- cd ../..
- cd frameworks/base
- git am ../../device/samsung/i9500/patches/frameworks_base/0001-DO-NOT-MERGE-PATCH-Zygote-Stop-breaking-the-entire-s.patch
- git fetch https://review.lineageos.org/LineageOS/android_frameworks_base refs/changes/45/169945/2 && git cherry-pick FETCH_HEAD
- cd ../..
- cd system/core
- git am ../../device/samsung/i9500/patches/system_core/79ce3d6a96f3d381dc4db1aac45ccb788e1276ab.patch
- cd ../..

4) You are good to go, proceed with the compiling process

- OPTIONAL (if you want built-in root support): export WITH_SU=true
- export WITH_TWRP=true

5) FOR GT-I9500 (ja3gxx) only. OTHERWISE, REPLACE THE CODENAME WITH OTHERS SUPPORTED (check the manifest).

- . build/envsetup && lunch lineage_ja3gxx-userdebug
- brunch lineage_ja3gxx-userdebug
