# golangのgRPCでの型説明

## string,bool,byte,int32,int64,uint32,uint64
## double
- 8byte小数
- Goでいうfloat64

## float
- 4byte小数
- Goでいうfloat32

## sint32
- 負の値があるときはこっちが効率的
- Goでいうint32

## sint64
- 負の値があるときはこっちが効率的
- Goでいうint64

## fixed32
- 4byte固定。 228を超える値の時unit32よりも効率的になることがある
- Goでいうuint32

## fixed64
- 8byte固定。 256を超える値の時unit64よりも効率的になることがある
- Goでいうuint64

## sfixed32
- 4byte固定
- Goでいうint32

## sfixed64
- 8byte固定
- Goでいうint64

# 型以外の説明

## repeated
- repeatedを型の前に付けると、そのフィールドは配列やリストのような扱いなる
- 多次元配列は定義できない
- `repeated string names = 1;`

## map
- キーと値の型を特定したマップを定義できる
- キーには整数値、文字列、真偽値のみ使える
- mapは配列にできない
- `map<string, string> test_map = 2;`

## enum
- 型の前にenumをつけることで列挙型を定義できる
- enumはデフォルトの値が0なので、必ずゼロ値を含めなければならない。
```
enum Kind {
    INFO = 0;
    WARN = 1;
    ERROR = 2;
}
message Log {
    Kind kind = 1;
}
```

## oneof
- 複数のフィールドのうち、どれか1つだけが選ばれるフィールド
- 以下はoneかotherを返すメッセージ型になる
```
oneof message {
    string one = 1;
    string other = 2;
}
```


[protobuf.dev](https://protobuf.dev/programming-guides/proto3/)
