# 网络请求

在 Android 开发中，进行网络请求是获取数据的重要方式。Android 提供了多种网络请求的库和框架，以下是常用的网络请求方式及其使用方法：

#### 1. **使用 HttpURLConnection**

这是 Android 内置的网络请求方式，适用于简单的 HTTP 请求。

**示例代码：**

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class NetworkRequest {
    public void getRequest() {
        Thread thread = new Thread(() -> {
            try {
                URL url = new URL("https://api.example.com/data");
                HttpURLConnection connection = (HttpURLConnection) url.openConnection();
                connection.setRequestMethod("GET");

                int responseCode = connection.getResponseCode();
                if (responseCode == HttpURLConnection.HTTP_OK) {
                    BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
                    String inputLine;
                    StringBuilder response = new StringBuilder();

                    while ((inputLine = in.readLine()) != null) {
                        response.append(inputLine);
                    }
                    in.close();
                    System.out.println("Response: " + response.toString());
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
        });
        thread.start();
    }
}
```

#### 2. **使用 Retrofit**

Retrofit 是一个强大的网络请求库，适合处理 RESTful API。它提供了简单的 API 调用方式和数据转换功能。

**添加依赖：**

在 `build.gradle` 中添加：

```gradle
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
implementation 'com.squareup.retrofit2:converter-gson:2.9.0' // 如果需要解析 JSON
```

**定义 API 接口：**

```java
import retrofit2.Call;
import retrofit2.http.GET;

public interface ApiService {
    @GET("data")
    Call<List<DataModel>> getData();
}
```

**使用 Retrofit 进行网络请求：**

```java
import retrofit2.Retrofit;
import retrofit2.converter.gson.GsonConverterFactory;

public class RetrofitClient {
    private static final String BASE_URL = "https://api.example.com/";
    private static Retrofit retrofit;

    public static Retrofit getClient() {
        if (retrofit == null) {
            retrofit = new Retrofit.Builder()
                    .baseUrl(BASE_URL)
                    .addConverterFactory(GsonConverterFactory.create())
                    .build();
        }
        return retrofit;
    }
}

// 在 Activity 或 Fragment 中使用
ApiService apiService = RetrofitClient.getClient().create(ApiService.class);
Call<List<DataModel>> call = apiService.getData();
call.enqueue(new Callback<List<DataModel>>() {
    @Override
    public void onResponse(Call<List<DataModel>> call, Response<List<DataModel>> response) {
        if (response.isSuccessful()) {
            List<DataModel> data = response.body();
            // 处理数据
        }
    }

    @Override
    public void onFailure(Call<List<DataModel>> call, Throwable t) {
        t.printStackTrace();
    }
});
```

#### 3. **使用 OkHttp**

OkHttp 是一个强大的 HTTP 客户端，适合用于执行网络请求。可以与 Retrofit 一起使用，也可以单独使用。

**添加依赖：**

在 `build.gradle` 中添加：

```gradle
implementation 'com.squareup.okhttp3:okhttp:4.9.3'
```

**使用 OkHttp 进行网络请求：**

```java
import okhttp3.Call;
import okhttp3.Callback;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;

public class OkHttpClientExample {
    private final OkHttpClient client = new OkHttpClient();

    public void getRequest() {
        Request request = new Request.Builder()
                .url("https://api.example.com/data")
                .build();

        client.newCall(request).enqueue(new Callback() {
            @Override
            public void onFailure(Call call, IOException e) {
                e.printStackTrace();
            }

            @Override
            public void onResponse(Call call, Response response) throws IOException {
                if (response.isSuccessful()) {
                    final String responseData = response.body().string();
                    // 处理响应数据
                }
            }
        });
    }
}
```

#### 4. **使用 Volley**

Volley 是 Google 提供的网络请求库，适合处理异步请求，特别是在需要处理图像加载和缓存时。

**添加依赖：**

在 `build.gradle` 中添加：

```gradle
implementation 'com.android.volley:volley:1.2.1'
```

**使用 Volley 进行网络请求：**

```java
import com.android.volley.Request;
import com.android.volley.RequestQueue;
import com.android.volley.Response;
import com.android.volley.VolleyError;
import com.android.volley.toolbox.StringRequest;
import com.android.volley.toolbox.Volley;

public class VolleyExample {
    public void getRequest(Context context) {
        RequestQueue queue = Volley.newRequestQueue(context);
        String url = "https://api.example.com/data";

        StringRequest stringRequest = new StringRequest(Request.Method.GET, url,
                new Response.Listener<String>() {
                    @Override
                    public void onResponse(String response) {
                        // 处理响应数据
                    }
                },
                new Response.ErrorListener() {
                    @Override
                    public void onErrorResponse(VolleyError error) {
                        error.printStackTrace();
                    }
                });

        queue.add(stringRequest);
    }
}
```

#### 小结

选择适合的网络请求方式取决于应用的需求。对于简单的请求，HttpURLConnection 或 OkHttp 是不错的选择；如果处理 RESTful API，Retrofit 是最佳选择；对于需要处理异步请求和缓存的场景，Volley 是理想的解决方案。



