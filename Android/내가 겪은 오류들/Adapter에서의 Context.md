# Adapter에서의 Context



RecyclerView나 ListView를 만들기 위해서는 Adapter를 이용해 데이터를 넣어준다.

이때  Adapter에서 Intent나 Toast 알림 처리 등을 할 때 Context를 사용해야한다.

Adapter에서는 Context가 안 만들어지기 때문에 view에서의 Context를 가져와야한다.



```java
public class CustomViewHolder extends RecyclerView.ViewHolder {
    protected TextView title, name, context;

    public CustomViewHolder(View view) {
        super(view);
        this.goBack = view.findViewById(R.id.back);

        goBack.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                //view에서의 context를 받아와서 이용한다.
                Intent intent = new Intent(view.getContext(), MainActivity.class);
                view.getContext().startActivity(intent);
            }
        });
    }
}
```



