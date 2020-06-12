# Retrofit2

Retrofit2 + oKHttp + Gson를 이용한 http api 통신 예제



## Service Interface

### getFirst

- @GET("/posts/{userId}") : GET 방식의 통신이며, [http://retrofit2.com/posts/{userId}의](http://jsonplaceholder.typicode.com/posts/%7BuserId%7D%EC%9D%98) 주소를 호출합니다.
- Call : ResponseGet형식으로 된 JSON을 통신을 통해 받습니다.
- @Path("userId") String id : id로 들어간 String 값을 1.에서 말한 {userId}로 넘겨줍니다. 즉 id에 "1"이라는 값이 들어가면 통신의 최종적인 주소는 <http://retrofit2.com/posts/1> 이 되는 것입니다.

### getSecond

- @GET("/posts") : 역시 GET 방식의 통신이며, [http://retrofit2.com/posts의](http://jsonplaceholder.typicode.com/posts%EC%9D%98) 주소를 호출합니다. Call<List> : 이번에는 ResponseGet형식으로 된 JSON 여러개를 통신을 통해 받습니다.
- @Qu프로젝트ery("userId") String id : getFirst와 달리 뒤에 붙는 파라미터가 없습니다. 이번 통신방식은 id에 "1"값이 들어가게 된다면 <http://retrofit2.com/posts?userId=1> 을 호출하는 것과 같은 형태를 띄게 됩니다. 여기서 @Query Annotation은 GET방식에서만 사용가능합니다.

### postFirst

- @POST("/posts") : POST 방식의 통신이며, 주소는 위와 같은 방식입니다.
- @FieldMap HashMap<String, Object> parameters : Field 형식을 통해 넘겨주는 값들이 여러개일 때 FieldMap을 사용합니다. Retrofit에서는 Map보다는 HashMap형식을 쓰기를 권장하고 있습니다.
- @FormUrlEncoded : Field 형식을 사용할 때는 Form이 Encoding되어야 합니다. 따라서 FormUrlEncoded라는 Annotation을 해주어야 합니다.
- @Field 형식의 경우에는 주로 POST 방식의 통신을 할때 사용합니다. GET 방식에서는 사용이 불가능합니다.

### putFirst

- @PUT("/posts/1") : PUT 방식의 통신이며, 주소는 위와 같은 방식입니다.
- @Body RequestPut parameters : 통신을 통해 전송하는 값이 특정 JSON 형식일 때 그러한 형태를 매번 만들지 않고 객체를 통해서 넘겨주는 방식입니다. 이러한 방식에서는 @Body라는 Annotation을 사용합니다. (PUT뿐만 아니라 다른 통신 방식에서도 마찬가지로 사용가능합니다)

### patchFirst

- @PATCH("/posts/1") : PATCH 방식의 통신이며, 주소는 위와 같은 방식입니다.
- @Field("title") String title : patch방식을 통해 title에 해당하는 값을 넘기기 위해 사용합니다.
- @FormUrlEncoded : 위에서의 설명과 같이 Field 형식을 사용하기에 추가해주어야합니다.

### deleteFirst

- @DELETE("/posts/1") : DELETE 방식의 통신이며, 주소는 위와 같은 방식입니다.
- Call : ResponseBody는 통신을 통해 되돌려 받는 값이 없을 경우 사용합니다.
- DELETE방식에서 @Body를 사용하기 위해선 다음처럼 해야합니다

```java
@HTTP(method = "DELETE", path = "/Arahant/Modification/Profile/Image/User", hasBody = true)
Call<ResponseBody> delete(@Body RequestGet parameters);
```



## Custom ResponseBody & RequestBody

## Retrofit Client

- 통신을 하기 위해서는 Retrofit Instance를 생성해야합니다.

## Retrofit CallBack

- retrofit의 통신은 background Thread에서 돌아갑니다. 이렇게 실행된 결과값을 UI Thread에서 사용하기 위해서는 CallBack 함수가 필요합니다.