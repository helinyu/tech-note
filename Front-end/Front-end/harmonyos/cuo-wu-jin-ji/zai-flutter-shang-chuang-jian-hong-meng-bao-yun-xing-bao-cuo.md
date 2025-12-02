# 在flutter上创建鸿蒙包运行报错

hvigor ERROR: 00303038 Configuration ErrorError Message: Schema validate failed, at file: /Users/hlym/workspace/aliyunxiao/dyy-app-front/ohos/entry/build-profile.json5

* Try the following:

Please check the following fields.{instancePath: 'buildOption',keyword: 'enum',params: {allowedValues: \['resOptions','externalNativeOptions','sourceOption','napiLibFilterOption','arkOptions','nativeLib','removePermissions','generateSharedTgz']},message: 'must be equal to one of the allowed values',location: '/Users/hlym/workspace/aliyunxiao/dyy-app-front/ohos/entry/build-profile.json5:4:19'}{instancePath: 'buildOption',keyword: 'propertyNames',params: { propertyName: 'useNormalizedOHMUrl' },message: 'property name must be valid',location: '/Users/hlym/workspace/aliyunxiao/dyy-app-front/ohos/entry/build-profile.json5:4:19'}

* Try:

Run with --stacktrace option to get the stack trace.Run with --debug option to get more log output.hvigor ERROR: BUILD FAILED in 871 msProcessException: The command failed with exit code 255Command: hvigorw assembleHap -p product=default -p buildMode=debug --no-daemon -pFLUTTER\_TARGET=/Users/hlym/workspace/aliyunxiao/dyy-app-front/lib/main.dart -p TARGET\_PLATFORM=ohos-arm64 -pDART\_DEFINES=RkxVVFRFUl9WRVJTSU9OPTMuMzIuNC1vaG9zLTAuMC4x,RkxVVFRFUl9DSEFOTkVMPVt1c2VyLWJyYW5jaF0=,RkxVVFRFUl9HSVRfVVJMPWh0dHBzOi8vZ2l0Y29kZS5jb20vb3Blbmhhcm1vbnktdHBjL2ZsdXR0ZXJfZmx1dHRlci5naXQ=,RkxVVFRFUl9GUkFNRVdPUktfUkVWSVNJT049NTg4ZWJlZmQwMQ==,RkxVVFRFUl9FTkdJTkVfUkVWSVNJT049OGNkMTllNTA5ZA==,RkxVVFRFUl9EQVJUX1ZFUlNJT049My44LjE= -p DART\_OBFUSCATION=false -pTRACK\_WIDGET\_CREATION=true -p TREE\_SHAKE\_ICONS=false -pPACKAGE\_CONFIG=/Users/hlym/workspace/aliyunxiao/dyy-app-front/.dart\_tool/package\_config.json
