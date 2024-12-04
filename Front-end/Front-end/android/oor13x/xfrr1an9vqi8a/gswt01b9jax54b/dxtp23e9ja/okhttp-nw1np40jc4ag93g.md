# okhttp网络请求

#### 1、权限处理

如果你的应用需要进行网络请求，请确保你在 `AndroidManifest.xml` 文件中声明了必要的权限：

```xml
xml复制代码<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```



**2、添加依赖：**

```gradle
gradle复制代码implementation "com.squareup.okhttp3:okhttp:4.9.3"
```



3、在Activity中写入代码：

```
 // 开启一个新的线程来执行网络请求
        new Thread(new Runnable() {
            @Override
            public void run() {
                OkHttpNetworkRequest okHttpNetworkRequest = new OkHttpNetworkRequest();
                try {
                    // 调用 sendGetRequest 方法进行网络请求
                    // 我们则个是get请求
                    String response = okHttpNetworkRequest.sendGetRequest("https://m.samh.xndm.tech/api/getconfig?area=CN&client-channel=appstore&gender=2&myuid=202709768&platform=android&platformname=google&productname=asmh&sessionid=&udid=DA90971F-6E45-460D-A45B-68F842282AB9&uid=202709768&version=3.5.0&vip_form=0");

                    // 网络请求返回后，更新UI（需要切换到主线程）
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
//                            textView.setText(response);
                            Log.d("lt -- NetworkResponse", response);
                        }
                    });

                } catch (IOException e) {
                    e.printStackTrace();

                    // 在 UI 线程中显示错误信息
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            Log.d("lt -- 请求失败: " , e.getMessage());
                        }
                    });
                }
            }
        }).start();
```
