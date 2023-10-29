# 대칭키 & 공개키 암호화

### ▶️ 암호화?

- 읽을 수 있는 데이터 → 이해할 수 없는 형태로 변환

### ▶️ 단방향 암호화 vs 양방향 암호화

- 단방향 암호화 : 원본 데이터 복원 불가
- 양방향 암호화 : 반대되는 복호화 과정을 사용하여 복원 가능

### ▶️ 대칭키

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1d40a623-da7d-44e1-9004-b5b5a8861918/aca7286d-cf48-4f48-a89e-50c2eaaec3ba/Untitled.png)

두 사람은 하나의 내용을 주고 받을 때 암호화 후 내용을 전달하고 복호화를 하여 읽게 된다.그리고 이 때 같은 키(`대칭키`)를 사용하는 방식이다. 이 경우 대칭키가 있게 되면 내용을 모두 읽을 수 있게 된다. 속도가 빠른 장점이 있지만 **만약 누군가가 이 대칭키를 악의적으로 가진다면 내용을 별다른 노력없이 볼 수 있게 된다.**

> 암호를 만드는 행위인 **암호화**를 할 때 사용하는 일종의 비밀번호를 키(key)라고 한다. 이 키에 따라서 암호화된 결과가 달라지기 때문에 키를 모르면 암호를 푸는 행위인 **복호화**를 할 수 없다. 대칭키는 동일한 키로 암호화와 복호화를 같이 할 수 있는 방식의 암호화 기법을 의미한다. 즉 암호화를 할 때 1234라는 값을 사용했다면 복호화를 할 때 1234라는 값을 입력해야 한다는 것이다.

### ▶️ 공개키

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1d40a623-da7d-44e1-9004-b5b5a8861918/a2208388-a083-4cb4-909f-fed99d4f6b41/Untitled.png)

- 공개키 암호: 암호로 사용될 경우 공개 공개키를 가지고 내용을 암호화 하게 됩니다. 그리고 이 내용은 private key를 가진 경우에만 열람이 가능해 집니다.
- 공개키 서명: 서명 용도로 사용 될 경우 private key를 가지고 암호를 하게 됩니다. 그리고 이 내용은 공개키를 통해 열 수 있게 되는데 이 경우 공개키를 가지는 누구나 이 내용을 열 수 있게 되지만 이 내용을 어느 쪽에서 서명 된 것인지 알 수 있게 됩니다. 브라우저에서는 이 방식을 사용하게 됩니다.

> 대칭키 방식은 단점이 있다. 암호를 주고 받는 사람들 사이에 대칭키를 전달하는 것이 어렵다는 점이다. 대칭키가 유출되면 키를 획득한 공격자는 암호의 내용을 복호화 할 수 있기 때문에 암호가 무용지물이 되기 때문이다. 이런 배경에서 나온 암호화 방식이 공개키방식이다.
>
> 공개키 방식은 두개의 키를 갖게 되는데 A키로 암호화를 하면 B키로 복호화 할 수 있고, B키로 암호화하면 A키로 복호화 할 수 있는 방식이다. 이 방식에 착안해서 두개의 키 중 하나를 비공개키(private key, 개인키, 비밀키라고도 부른다)로하고, 나머지를 공개키(public key)로 지정한다. 비공개키는 자신만이 가지고 있고, 공개키를 타인에게 제공한다. 공개키를 제공 받은 타인은 공개키를 이용해서 정보를 암호화한다. 암호화한 정보를 비공개키를 가지고 있는 사람에게 전송한다. 비공개키의 소유자는 이 키를 이용해서 암호화된 정보를 복호화 한다. 이 과정에서 공개키가 유출된다고해도 비공개키를 모르면 정보를 복호화 할 수 없기 때문에 안전하다. 공개키로는 암호화는 할 수 있지만 복호화는 할 수 없기 때문이다.
>
> 이 방식은 이렇게 응용할 수도 있다. 비공개키의 소유자는 비공개키를 이용해서 정보를 암호화 한 후에 공개키와 함께 암호화된 정보를 전송한다. 정보와 공개키를 획득한 사람은 공개키를 이용해서 암호화된 정보를 복호화 한다. 이 과정에서 공개키가 유출된다면 의도하지 않은 공격자에 의해서 데이터가 복호화 될 위험이 있다. 이런 위험에도 불구하고 비공개키를 이용해서 암호화를 하는 이유는 무엇일까? 그것은 이것이 데이터를 보호하는 것이 목적이 아니기 때문이다. 암호화된 데이터를 공개키를 가지고 복호화 할 수 있다는 것은 그 데이터가 공개키와 쌍을 이루는 비공개키에 의해서 암호화 되었다는 것을 의미한다. 즉 공개키가 데이터를 제공한 사람의 신원을 보장해주게 되는 것이다. 이러한 것을 전자 서명이라고 부른다.