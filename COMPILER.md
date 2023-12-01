### FFmpeg source code origin

Find the proper description on the separate page.

Desired ABIs to build

    --target-abis=xxx or -abis=xxx

Specifies desired ABIs to build. The value of the flag is an enumeration of ABIs separated by comma.

Supported values:

    x86
    x86_64
    armeabi-v7a or arm
    arm64-v8a or arm64

Order of specified ABIs matters, as they will be built in the same order.

If neither argument is specified at all then the FFmpeg will be built for all 4 ABIs.

Examples:

    ./ffmpeg-android-maker.sh -abis=arm,arm64
    
    ./ffmpeg-android-maker.sh --target-abis=armeabi-v7a,x86
    
    ./ffmpeg-android-maker.sh -abis=armeabi-v7a,arm64-v8a,x86,x86_64

### Builds binaries for all 4 ABIs

    ./ffmpeg-android-maker.sh
Android platform version

--android-api-level=x or -android=x

Specifies the Android API level to compile against. Newer versions of Android support wider API.

The minimum supported value is 16. It is constrained by Android NDK, as it doesn't support lower APIs anymore.

Regardless of specified value, 64 bit ABIs (arm64-v8a and x86_64) have minimum value of 21 (as Android 5 is the first one that has 64 bit support). If specified flag value is greater than 21, then it is used for all ABIs.

For example:

    When -android=19, then 32 bit ABIs are compiled against API 19 and 64 bit ABIs are compiled agains API 21.
    When -android=24, then all ABIs are compiled agains API 24.
    The default value is 19. With NDK r23 it is still possible to use 16. Starting with NDK r24 APIs 16-18 will be removed;

Sometimes this argument is helpful. For example the encoder of libaom requires API 18. Building only a decoder from this library allows using API 16.

Examples:

    # API 19 is used for 32 bit ABIs and API 21 for 64 bit ABIs
    ./ffmpeg-android-maker.sh -android=19
    
    # API 24 is used for all ABIs
    ./ffmpeg-android-maker.sh --android-api-level=24
    
    # API 16 is used for 32 bit ABIs and API 21 for 64 bit ABIs
    ./ffmpeg-android-maker.sh 