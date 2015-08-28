PROJECT_PATH = "./cocos2d_libs.xcodeproj"
TARGET_NAME="'libcocos2d iOS'"
OUTPUT_DEBUG="tmp/iphonesimulator"
OUTPUT_RELEASE="tmp/iphoneos"
OUTPUT_LIB="./lib"
directory OUTPUT_LIB

desc "using lib command to build a static library"
task "lib" do
    sh "xcodebuild -project #{PROJECT_PATH} -configuration Release -sdk iphonesimulator8.4 -target #{TARGET_NAME} -arch i386 -arch x86_64 TARGET_BUILD_DIR=#{OUTPUT_DEBUG} BUILT_PRODUCTS_DIR=#{OUTPUT_DEBUG} clean build"

    sh "xcodebuild -project #{PROJECT_PATH} -configuration Release -sdk iphoneos8.4 -target #{TARGET_NAME} -arch armv7 -arch armv7s -arch arm64 TARGET_BUILD_DIR=#{OUTPUT_RELEASE} BUILT_PRODUCTS_DIR=#{OUTPUT_RELEASE} clean build"
end

desc "using lipo command to link static libraries for each device to one combined library file"
task "lipo" => OUTPUT_LIB do

    Dir.glob("#{OUTPUT_RELEASE}/*"){|path|
        p path
        file = File.basename(path)

        sh "lipo '#{OUTPUT_DEBUG}/#{file}' '#{OUTPUT_RELEASE}/#{file}' -create -output '#{OUTPUT_LIB}/#{file}'"
    }
end
