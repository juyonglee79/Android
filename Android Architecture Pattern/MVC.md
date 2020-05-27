# MVC

> Both the Controller and the View depend on the Model: the Controller to update the data, the View to get the data.

#### 등장시기

- 그래픽 사용자 인터페이스의 초기 개발에 대한 통찰력 중 하나이다.
- MVC는 책임과 관련하여 소프트웨어 구성을 설명하고 구현하는 첫 번째 방법 중 하나가 되었다.
- Trygve Reenskaug는 1970 년대에 Xerox Palo Alto Research Center(PARC)를 방문하면서 Smalltalk -76에 MVC를 도입했다.

#### 등장이유

- 사용자 인터페이스 로직이 비즈니스 로직보다 자주 변경되는 경향이 있는 세계
- **각 계층을 분리**시킴으로써 **코드의 재활용성을 높이고 불필요한 중복을 막기**위해서

#### 정의

- Model : 비즈니스 계층 관리. 네트워크 또는 데이터베이스 API를 처리하는 **데이터 계층**
- View : 모델의 데이터를 시각화. 즉, UI Layer.
- Controller : Logic Layer은 사용자 행동을 통지 받고 필요에 따라 모델을 업데이트함.

#### 특징

- Model

  - 정의와 같다.

- View

  - 뷰는 하위 모델에 대한 지식이나 상태에 대한 이해가 없고, 사용자가 버튼을 클릭하거나 값을 입력하는 등의 행동을 할 때 무엇을 해야 하는지 모른다.

    > 뷰가 덜 알수록 모델에 종속되지 않으므로 보다 변화에 유연할 수 있다.

- Controller

  - 앱을 묶어주는 **접착제**

  - 뷰가 컨트롤러에게 사용자가 버튼을 눌렀다고 알리면, 컨트롤러는 그에 따라 어떻게 모델과 상호작용할지 결정한다.

  - 모델에서 데이터가 변화되는 것에 따라 컨트롤러는 뷰의 상태를 적절하게 업데이트하도록 결정할 수 있다.

  - 안드로이드 앱에서는 컨트롤러가 주로 액티비티나 프래그먼트로 표현된다.

    

#### 장점

- 코드의 테스트 가능성이 향상된다.

- 확장이 용이하여 새로운 기능을 쉽게 구현할 수 있다.

- Model 클래스는 Android 클래스에 대한 참조가 없으므로 단위 테스트에 가능하다. 마찬가지로 Controller의 단위테스트도 가능하다.

  

- -모델이 어디에도 종속되지 않으며, 뷰는 유닛 테스트 레벨에서 그다지 테스트할 것이 거의 없어서 쉽게 모델을 테스트할 수 있다. 확장이 용이하여 새로운 기능을 쉽게 구현할 수 있다.

  

#### 단점

- View가 Controller와 Model 모두에 의존한다는 점을 감안할 때, UI Logic의 변경은 여러 클래스의 업데이트가 필요할 수 있으므로 패턴의 유연성이 떨어진다.

  

- View와 Model이 서로 의존적이다.

  

#### Controller 단점

- **테스트 용이성** : 컨트롤러가 안드로이드 API에 깊게 종속되므로 유닛 테스트가 어렵습니다.
- **모듈화 및 유연성** : 컨트롤러가 뷰에 단단히 결합되며, 뷰의 확장일 수도 있습니다. 뷰를 변경하면 컨트롤러로 돌아가서 변경해야 합니다.
- **유지 보수** : 시간이 지남에 따라 보다 많은 코드가 컨트롤러로 모이면서 비대해지고 문제가 발생하기 쉬워집니다. 특히 *anemic models 모델을 사용하는 앱에서라면 더욱 그렇습니다.

*anemic models ?

빈약한 도메인 모델. 모든 도메인 로직이 서비스 계층에 있다면, 여러분은 스스로를 장님으로 만든 것이나 다름없다.

#### 예제 코드

```
public class MainActivity extends AppCompatActivity {
    private MainModel mainModel;
    private TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mainModel = new MainModel();

        textView = (TextView) findViewById(R.id.btn_confirm);
        textView.setText("Non-Clicked");

        findViewById(R.id.btn_confirm).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String text = mainModel.getClickedText();
                TextView textView = (TextView) findViewById(R.id.btn_confirm);
                textView.setText(mainModel.getClickedText());
            }
        });
    }

}
public class MainModel {
    public String getClickedText() {
        return "Clicked!!!";
    }
}
```

## 1-1. Passive Model

### 1-1-1. 특징

- Controller는 Model을 조작하는 유일한 클래스.

- 사용자의 동작에 따라 Controller는 Model을 수정해야 한다.

- Model이 업데이트 된 후에 Controller는 View를 업데이트해야 함을 알린다. View는 Model로부터 데이터를 요청한다.

  

## 1-2. Active Model

### 1-2-1. 특징

- Controller는 Model을 수정하는 유일한 클래스가 아닌 경우 모델은 **Observer Pattern**의 도움을 받아 View 및 기타 클래스에 업데이트를 알린다.
- Model에는 업데이트에 관심이 있는 Observer 컬렉션이 포함되어 있다.
- View는 Observer interface를 구현하고 Observer를 Model에 등록한다.
- Model이 업데이트 될 때마다 Observer 컬렉션을 반복하여 update메소드를 호출한다. View에서 이 메소드를 구현하면 Model의 최신 데이터 요청이 트리거된다.





### 참고문서

* https://medium.com/upday-devs/android-architecture-patterns-part-1-model-view-controller-3baecef5f2b6

