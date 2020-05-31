# MVVM

> The MVVM pattern was created to simplify the event driven programming of user interfaces.

#### 등장시기

 Activity(Fragment)가 View 와 Controller 두 가지의 특성을 모두 가지고 있기 때문에 View나Controller를 한 쪽으로 빼게 될 경우 View에 대한 바인딩이나 처리에서 중복 코드나 일관성을 잃어버리는 코드를 작성할 수 있다. 이를 개선하기 위해서 MVVM 이란 패턴이 등장했다.

#### 정의

- Model(Data Model)
  - 데이터 소스를 추상화한다.
  - View Model은 Data Model과 함께 작동하여 데이터를 가져오고 저장한다.
- View
  - 사용자의 행동에 대한 뷰 모델을 알린다.
- View Model
  - View에 관련 데이터의 스트림을 노출한다.

#### 특징

> 안드로이드 데이터 바인딩을 사용하는 MVVM은 테스트와 모듈화가 쉽고 뷰와 모델을 연결하기 위해
>
> 사용해야 하는 연결 코드를 줄일 수 있다는 장점이 있다.

- ViewModel에는 View에 대한 정보가 없다.

  

- Model

  - MVC와 동일하며 변화가 없다.

- View

  - 뷰는 뷰모델에 의해 보여지는 옵저버블 변수와 액션에 유연하게 바인딩된다.

- ViewModel

  - 뷰모델은 모델을 래핑하고 뷰에 필요한 옵저버블 데이터를 준비한다.

  - 뷰가 모델에 이벤트를 전달할 수 있도록 훅(hook)을 준비한다. 그러면서도 뷰모델이 뷰에 종속되지는 않는다.

    

#### 장점

- 테스트 하기가 쉽다.
- UI 요구사항이 다시 변경되면 쉽게 바꿀 수 있다.

#### 단점

- Activity와 Fragment의 코드가 많아질수록 유지보수가 어렵다.

- 중첩된 콜백이 많으면 코드를 변경하거나 새로운 기능을 추가하기 어렵고 이해하기가 어렵다.

- Activity와 Fragment에 많은 로직들이 구현되어 있어 유닛 테스팅은 가능하지만 어렵다.

  

#### 예제 코드

```java
public class MainActivity extends AppCompatActivity {
    private MainViewModel mainViewModel;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mainViewModel = new MainViewModel(MainActivity.this);
    }

}
public class MainModel {
    public String getClickedText() {
        return "Clicked!!!";
    }
}
public class MainViewModel {
    private Activity activity;
    private MainModel mainModel;
    private TextView textView;


    public MainViewModel(Activity activity) {
        this.activity = activity;
        this.mainModel = new MainModel();
        initView(activity);
    }

    private void initView(Activity activity) {
        textView = (TextView) activity.findViewById(R.id.btn_confirm);
        textView.setText("Non-Clicked");

        activity.findViewById(R.id.btn_confirm)
                .setOnClickListener(new View.OnClickListener() {
                    @Override
                    public void onClick(View view) {
                        String text = mainModel.getClickedText();
                        textView.setText(text);
                    }
                });
    }
}
```