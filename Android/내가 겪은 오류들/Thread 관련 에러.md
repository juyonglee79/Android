# Thread 관련 에러

> ## Only the original thread that created a view hierarchy can touch its views

##### Error Code

android.view.ViewRootImpl$CalledFromWrongThreadException: 

Only the original thread that created a view hierarchy can touch its views.



##### 해석

Original Thread으로만 UI(view heirarchy: 화면 체계)를 변경시킬 수 있다.



##### 원인 

Main Thread 외의 새로 생성한 Thread를 이용하여 임의로 UI를 변경시키려고 했기 때문이에요. 



##### 해결 방법 

Handler를 이용하여 Main Thread를 간접적으로 사용하면 해결할 수 있습니다.



final Handler handler = new Handler(){
    public void handleMessage(Message msg){
        // 원래 하려던 동작 (UI변경 작업 등)
    }
};

```
Timer timer = new Timer(true);
TimerTask timerTask = new TimerTask() {
    @Override
    public void run() {
        Log.v(TAG,"timer run");
        Message msg = handler.obtainMessage();
        handler.sendMessage(msg);
    }

    @Override
    public boolean cancel() {
        Log.v(TAG,"timer cancel");
        return super.cancel();
    }
};
timer.schedule(timerTask, 0, 1000);
```



위의 코드를 보면 알 수 있듯,

Handler를 생성해서 원하는 동작을 선언해 놓고, 

Timer를 카운트 할 때마다 handler를 작동시키는 것을 볼 수 있다.



 간결하게 표현하면

Handler handler = new Handler(){

​	public void handleMessage(Messaage msg){

​		// 내가 원하는 UI 변경 작업!!

​	}

}



##### 코드 Run하는 중 UI 동작 변경하고 싶을 때 

Message msg = handler.obtainMessage();

handler.sendMessage(msg);

해당 동작의 handler를 호출하면 된다.