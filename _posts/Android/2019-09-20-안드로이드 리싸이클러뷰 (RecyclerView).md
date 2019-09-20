---
title: "안드로이드 리사이클러뷰(RecyclerView)"
categories: 
  - Android
last_modified_at: 2019-09-20T13:00:00+09:00
tags: 
  - Android
  - Java


toc: true
sidebar_main: true
---

## Intro

> 안드로이드 Recyclerview 알아보기


## RecyclerView

`RecyclerView`는 데이터의 집합을 좀더 유연하게 표시 할 수 있도록 만들어주는 위젯이다. 

`ListView`와 유사하지만 생성된 View를 재활용(Recycle)하여 사용하며 아이템들을 수직,수평 등 동적 구성을 원할하게 할 수 있어 유연함과 성능을 개선했다.




## RecyclerView 구성요소

> Adapter

데이터들을 아이템 단위의 뷰를 구성하기위한 뷰 생성을 담당한다.

> Layout Manager

아이템뷰가 나열되는 형태를 관리하는 역할을 한다.

또한 화면에 표시되지 않는 아이템 뷰를 언제 재활용 할 것인지도 결정

## RecyclerView 구현하기

> 아이템 뷰 레이아웃 추가

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/recyclerview/1.png?raw=true)

아이템이 될 XML 작성


> 어댑터 구현

리사이클러뷰가 사용할 어댑터를 `RecyclerView.Adapter`를 상속받아 구현한다.

상속시 반드시 다음 메서드를 오버라이드 해야한다.

`onCreateViewHolder` , `onBindViewHolder` , `getItemCount`

```java

public class TextAdapter extends RecyclerView.Adapter<TextAdapter.ViewHolder>
{
    private ArrayList<String> mData = null;

    // 생성자
    public TextAdapter(ArrayList<String> list)
    {
       mData = list;
    }
    
    // ViewHolder (화면에 표시될 아이템뷰 저장)
    public class ViewHolder extends RecyclerView.ViewHolder
    {
        public TextView textView1;

        ViewHolder(View itemView)
        {
            super(itemView);

            textView1 = itemView.findViewById(R.id.text1);
        }
    }


    // 아이템 뷰를 위한 뷰홀더 객체를 생성하고 리턴
    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType)
    {
        Context context = parent.getContext();
        LayoutInflater inflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);

        View view = inflater.inflate(R.layout.recyclerview_item, parent, false);
        TextAdapter.ViewHolder vh = new TextAdapter.ViewHolder(view);

        return vh;
    }


    // position에 해당되는 데이터를 뷰홀더의 아이템뷰에 표시
    @Override
    public void onBindViewHolder(@NonNull ViewHolder holder, int position)
    {
        String text = mData.get(position);
        holder.textView1.setText(text);
    }


    @Override // 데이터 갯수 리턴
    public int getItemCount()
    {
        return mData.size();
    }

}


```

> 리사이클러뷰 어댑터 레이아웃 매니저 지정

```java
public class Frag2 extends Fragment
{

    public static final int REQUEST_CODE_INSERT = 1000;
    private View view;
    private TextView mTextDate;
    private SimpleDateFormat mFormat = new SimpleDateFormat("yyyy/M/d"); 
    private String mTime;
    private RecyclerView recyclerView;
    private TextAdapter textAdapter;
    private MemoDBHelper dbHelper;
    private ArrayList<String> list;

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState)
    {
        view = inflater.inflate(R.layout.frag2, container, false);
        
        list = new ArrayList<>();
        recyclerView = (RecyclerView) view.findViewById(R.id.recycler1);


        Date date = new Date();
        mTime = mFormat.format(date);


        dbHelper = MemoDBHelper.getInstance(getActivity());


        // 리사이클러뷰 LinearLayoutManager 객체 지정
        recyclerView.setLayoutManager(new LinearLayoutManager(getActivity()));

        // 어댑터 객체 생성
        textAdapter = new TextAdapter(list);

        // DB 에서 list 값저장
        getMemoCursor();

        // recyclerView 어댑터 객체 지정
        recyclerView.setAdapter(textAdapter);

        return view;
    }

    // 커서의 데이터를 Arraylist에 저장하는 메서드
    private void getMemoCursor()
    {
        String[] params = {mTime};
    
        list.clear();

        Cursor cursor = dbHelper.getReadableDatabase().query(MemoContract.MemoEntry.TABLE_NAME, null, "date=?", params, null, null, null);

        while (cursor.moveToNext())
        {
            list.add(cursor.getString(cursor.getColumnIndex(MemoContract.MemoEntry.COLUMN_NAME_TITLE)));
        }

        textAdapter.notifyDataSetChanged();
    }
```
리사이클뷰의 레이아웃 매니저(LinearLayout)을 지정하고
`List`를 어댑터 객체 생성과 함께 `List`를 어댑터 클래스에 전달한다음 데이터베이스에서 불러온 데이터를 리스트에 담은 다음 어댑터를 지정해주면 아이템뷰가 생성되어 표시된다.

이때 새로운 데이터가 추가,삭제 됐을때 `Adapter.notifyDataSetChanged()`를 통해 갱신해줄 수 있다.

## 실행 결과

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/recyclerview/2.png?raw=true)

## 참고자료

[https://recipes4dev.tistory.com/154](https://recipes4dev.tistory.com/154)

