#  MVP

> Since the View and the Presenter work closely together, they need to have a reference to one another. To make the Presenter unit testable with JUnit, the View is abstracted and an interface for it used. The relationship between the Presenter and its corresponding View is defined in a `Contract` interface class, making the code more readable and the connection between the two easier to understand.

#### 등장시기

- MVC 패턴의 단점을 보완하기 위하여 등장한 패턴.

- MVC 패턴은 뷰가 모델에 강력하게 의존한다. MVP는 각 요소를 명확하게 분리하여 커플링을 낮추기 위해 등장했다.

  

#### 정의

- Model

  - MVC와 같다.

- View

  - MVC와 같다.

- Controller

  - 모델에서 데이터를 검색.
  - UI로직 적용.
  - View 상태 관리 및 표시 할 항목 결정.
  - View에서 사용자 입력 통지에 반응.

  

#### 특징

> MVP는 컨트롤러의 책임에 묶이지 않고도 뷰와 액티비티가 자연스럽게 결합하도록 한다.

- Presenter은 View에서 분리되어 있다. View를 interface를 통해 조작한다. 그래서 View를 *Mock하여 테스트하기 쉽다.

- Controller와 View가 모두 모델에 따라 다르다.

- Controller는 데이터를 업데이트한다.

- View는 데이터를 가져온다.

  

- Model

  - MVC와 동일하며 변화가 없다.

- View

  - 변화 : 액티비티/프래그먼트가 이제 뷰의 일부로 간주된다는 것이다.

    > 따라서 이들이 서로에게 연관되는 자연스러운 현상을 극복할 필요가 없다.

  - 액티비티가 뷰 인터페이스를 구현해서 프리젠터가 코드를 만들 인터페이스를 갖도록 하는 것이 좋다.

    > 특정 뷰와 결합되지 않고 가상 뷰를 구현해서 간단한 유닛 테스트를 실행할 수 있다.

- Presenter

  - 본질적으로는 MVC의 컨트롤러와 같지만, 뷰에 연결되는 것이 아니라 그냥 인터페이스라는 점이 다르다.

    > MVC가 가진 테스트 가능성 문제와 함께 모듈화/유연성 문제 역시 해결합니다.

  

### Mocking ?

- 종속성에 의존하지 않고 코드 단위를 테스트 할 수있게 해주는 하나의 특정 기술이다.
- 일반적으로 다른 메소드와 차이점은 코드 의존성을 대체하는 모의 객체(Mocking)가 기대치를 설정할 수 있다는 것이다. 모의 객체(Mocking)는 코드에 의해 호출되는 방법과 응답하는 방법을 알게된다.

#### 장점

- 매우 훌륭한 분리를 제공한다.

  

#### 단점

- 작은 어플 or 프로토 타입 개발 시, 오버 헤드처럼 보일 수 있다. (사용되는 인터페이스가 많기 때문에)

- Presenter가 모든 것을 아는 클래스가 된다. 그러나 이는 코드를 더 많이 분해하고, 단위 테스트가 가능한 클래스를 만들면 된다.

  

#### 예제 코드

```java
public interface MainPresenter {
    void setView(MainPresenter.View view);

    void onConfirm();

    public interface View {
        void setConfirmText(String text);
    }
}
public class MainActivity extends AppCompatActivity implements MainPresenter.View{
    private MainPresenter mainPresenter;
    private Button confirmButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mainPresenter = new MainPresenterTmpl(MainActivity.this);
        mainPresenter.setView(this);

        confirmButton = (Button) findViewById(R.id.btn_confirm);
        confirmButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                mainPresenter.onConfirm();
            }
        });
    }

    @Override
    public void setButtonText(String text) {
        confirmButton.setText(text);
    }
}
public class MainModel {
    public String getClickedText() {
        return "Clicked!!!";
    }
}
public class MainPresenterTmpl implements MainPresenter {
    private Activity activity;
    private MainPresenter.View view;

    public MainPresenterTmpl(Activity activity) {
        this.activity = activity;
        this.mainModel = new MainModel();
    }

    @Override
    public void setView(View view) {
        this.view = view;
    }

    @Override
    public void onConfirm() {
        if(view!=null) {
            view.setConfirmText(mainModel.getClickedText());
        }
    }
}
```