# 网络库添加

在 Android Java 中配置网络库通常涉及选择一个合适的网络请求库，然后在 `build.gradle` 文件中进行配置。以下是几种常见的网络库以及它们的配置方法：

#### 1. 使用 **OkHttp** 库

**OkHttp** 是一个非常流行的 HTTP 客户端，支持同步和异步请求。可以用于执行网络请求、处理缓存、处理连接池等。

**配置 OkHttp：**

1.  **在 `build.gradle` 中添加依赖：**

    在项目的 `app` 级别 `build.gradle` 文件中的 `dependencies` 部分添加 OkHttp 库的依赖。

    ```gradle
    dependencies {
        implementation 'com.squareup.okhttp3:okhttp:4.10.0' // 版本可以根据需要调整
    }
    ```
2.  **使用 OkHttp 进行网络请求：**

    ```java
    import okhttp3.OkHttpClient;
    import okhttp3.Request;
    import okhttp3.Response;

    public class MyNetworkClient {
        public static void fetchData() {
            OkHttpClient client = new OkHttpClient();
            Request request = new Request.Builder()
                    .url("https://jsonplaceholder.typicode.com/posts")
                    .build();

            client.newCall(request).enqueue(new okhttp3.Callback() {
                @Override
                public void onFailure(okhttp3.Call call, IOException e) {
                    // 处理失败的情况
                    e.printStackTrace();
                }

                @Override
                public void onResponse(okhttp3.Call call, Response response) throws IOException {
                    if (response.isSuccessful()) {
                        String responseData = response.body().string();
                        // 处理成功的响应
                        Log.d("NetworkResponse", responseData);
                    }
                }
            });
        }
    }
    ```

#### 2. 使用 **Retrofit** 库

**Retrofit** 是一个更高层次的 HTTP 客户端，通常与 Gson、Moshi 等库结合使用，能够将 JSON 数据解析为 Java 对象。

**配置 Retrofit：**

1.  **在 `build.gradle` 文件中添加依赖：**

    在 `dependencies` 部分添加 Retrofit 和 Gson 转换器的依赖。

    ```gradle
    dependencies {
        implementation 'com.squareup.retrofit2:retrofit:2.9.0' // Retrofit
        implementation 'com.squareup.retrofit2:converter-gson:2.9.0' // Gson 转换器
    }
    ```
2.  **创建接口和 Retrofit 实例：**

    定义一个接口来描述 API 请求。

    ```java
    import retrofit2.Call;
    import retrofit2.http.GET;

    public interface ApiService {
        @GET("posts")
        Call<List<Post>> getPosts();
    }
    ```

    然后，创建 Retrofit 实例并发起请求：

    ```java
    import retrofit2.Retrofit;
    import retrofit2.converter.gson.GsonConverterFactory;
    import retrofit2.Callback;
    import retrofit2.Response;

    public class NetworkClient {
        private static final String BASE_URL = "https://jsonplaceholder.typicode.com/";

        public static void fetchPosts() {
            Retrofit retrofit = new Retrofit.Builder()
                    .baseUrl(BASE_URL)
                    .addConverterFactory(GsonConverterFactory.create())
                    .build();

            ApiService apiService = retrofit.create(ApiService.class);
            Call<List<Post>> call = apiService.getPosts();

            call.enqueue(new Callback<List<Post>>() {
                @Override
                public void onResponse(Call<List<Post>> call, Response<List<Post>> response) {
                    if (response.isSuccessful()) {
                        List<Post> posts = response.body();
                        // 处理响应数据
                    }
                }

                @Override
                public void onFailure(Call<List<Post>> call, Throwable t) {
                    // 处理失败的情况
                }
            });
        }
    }
    ```

    需要根据你的项目中实际的实体类 `Post` 和 API URL 做相应的调整。

#### 3. 使用 **Volley** 库

**Volley** 是 Google 官方提供的一个网络请求库，提供了非常简便的 API 进行 HTTP 请求的处理，支持异步请求、图片加载等功能。

**配置 Volley：**

1.  **在 `build.gradle` 中添加依赖：**

    ```gradle
    dependencies {
        implementation 'com.android.volley:volley:1.2.1'  // Volley 库的版本
    }
    ```
2.  **使用 Volley 发起请求：**

    ```java
    import com.android.volley.Request;
    import com.android.volley.RequestQueue;
    import com.android.volley.toolbox.JsonObjectRequest;
    import com.android.volley.toolbox.Volley;
    import org.json.JSONObject;

    public class NetworkRequest {
        private RequestQueue requestQueue;

        public void fetchData(Context context) {
            requestQueue = Volley.newRequestQueue(context);
            String url = "https://jsonplaceholder.typicode.com/posts";

            JsonObjectRequest jsonObjectRequest = new JsonObjectRequest(Request.Method.GET, url, null,
                response -> {
                    // 处理响应
                    Log.d("VolleyResponse", response.toString());
                },
                error -> {
                    // 处理错误
                    Log.e("VolleyError", error.toString());
                });

            requestQueue.add(jsonObjectRequest);
        }
    }
    ```

#### 总结：

* **OkHttp** 是最基础的 HTTP 客户端，适合需要高度自定义的场景。
* **Retrofit** 是基于 OkHttp 的更高级封装，适合做 RESTful API 的调用，并且支持自动化的 JSON 解析。
* **Volley** 是 Android 官方提供的库，简化了请求和响应的处理，适合不需要复杂配置的应用。



方案： 选择了OKHttp + **Retrofit 来实现的。**
