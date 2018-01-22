
# SSZipArchive

ZipArchive is a simple utility class for zipping and unzipping files on iOS, macOS and tvOS.

- Unzip zip files;
- Unzip password protected zip files;
- Unzip AES encrypted zip files;
- Create zip files;
- Create password protected zip files;
- Create AES encrypted zip files;
- Choose compression level;
- Append to existing zip files;
- Zip-up NSData instances. (with a filename)

This fork adds the ability to handle output of ZipArchive as NSData chunks and stream it over network or so.
It also provides manual access to zip entries for large files.

## Installation and Setup

*The main release branch is configured to support Objective C and Swift 3+.*

SSZipArchive works on Xcode 7-9 and above, iOS 8-11 and above.

### CocoaPods
In your Podfile:  
`pod 'SSZipArchive'`

### Carthage
In your Cartfile:  
`github "ZipArchive/ZipArchive"`

### Manual

1. Add the `SSZipArchive` and `minizip` folders to your project.
2. Add the `libz` library to your target

SSZipArchive requires ARC.

## Usage

### Objective-C

```objective-c
// Create
[SSZipArchive createZipFileAtPath:zipPath withContentsOfDirectory:sampleDataPath];

// or to delegate
[SSZipArchive createZipWithIODelegate:self
              withContentsOfDirectory:sampleDataPath
              keepParentDirectory:NO
              compressionLevel:-1
              password:password.length > 0 ? password : nil
              AES:YES
              progressHandler:nil];

// handle write delegate
- (uint32_t)zipArchiveDidWriteData:(NSData *)data {    
    // e.g. write data stream to a file
    // [_zipfile writeData:data];
    
    return (uint32_t)[data length];
}

- (void)zipArchiveDidClose {
    // e.g. close file
    // [_zipfile closeFile];
}

// Unzip
[SSZipArchive unzipFileAtPath:zipPath toDestination:unzipPath];
```

### Swift

```swift
// Create
SSZipArchive.createZipFileAtPath(zipPath, withContentsOfDirectory: sampleDataPath)

// Unzip
SSZipArchive.unzipFileAtPath(zipPath, toDestination: unzipPath)
```

## License

SSZipArchive is protected under the [MIT license](https://github.com/samsoffes/ssziparchive/raw/master/LICENSE) and our slightly modified version of [Minizip](https://github.com/nmoinvaz/minizip) 1.2 is licensed under the [Zlib license](http://www.zlib.net/zlib_license.html).

## Acknowledgments

* Big thanks to [aish](http://code.google.com/p/ziparchive) for creating [ZipArchive](http://code.google.com/p/ziparchive). The project that inspired SSZipArchive.
* Thank you [@soffes](https://github.com/soffes) for the actual name of SSZipArchive.
* Thank you [@randomsequence](https://github.com/randomsequence) for implementing the creation support tech.
* Thank you [@johnezang](https://github.com/johnezang) for all his amazing help along the way.
