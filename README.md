# CustomWidget
도형님 스터디로 custom widget을 구현해봤습니다.

```

public class Today extends TextView {

    public Today(Context context, AttributeSet attrs) {
        super(context, attrs);

        // # 커스텀 위젯에 커스텀 속성 사용하기
        // 1. res/values/attrs.xml에 정의된 어트리뷰트를 가져온다.
        TypedArray typed = context.obtainStyledAttributes(attrs, R.styleable.Today);

        // 2. 해당 이름으로 정의된 속성의 개수를 가져오고
        int size = typed.getIndexCount();

        // 3. 반복문을 돌면서 해당 속성에 대한 처리를 해준다.
        for(int i=0; i<size ; i++) {
            // 3.1 현재 속성의 아이디 가져오기
            int currentAttr = typed.getIndex(i);
            switch (currentAttr) {
                // 3.2 아이디가 attrs.xml에 정의된 속성아이디와 같다면
                case R.styleable.Today_delimeter:
                    // 3.3 현재 속성에 입력되어 있는 값을 꺼낸다
                    String delimeter = typed.getString(currentAttr);
                    setDate(delimeter);
                    break;
            }
        }

    }

    private void setDate(String delimeter) {
        // 날짜를 가져오는 함수
        Calendar cal = Calendar.getInstance();
        // 날짜 포맷을 정의하는 함수
        Date today = cal.getTime();
        //포매터를 이용한 날짜포맷 변경
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy" + delimeter + "MM" + delimeter + "dd");


        // this.setText 해야하는데 어차피 textview를 상속받은 객체이므로 그냥 setText해도무방.
        setText(sdf.format(today));
    }

}

```
