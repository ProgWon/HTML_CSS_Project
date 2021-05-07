## 접근성 위반 사항
|접근성 위반 내용|	관련 지침|
|-------------|------|
|대체 텍스트 제공x|	1.1.1 비텍스트 컨텐츠
|정보와 구조 관계 제공x|	1.3.1 정보와의 관계
|레이블의 주제 설명 제공x|	2.4.6 제목과 레이블
|키보드 포커스 표시 x|2.4,7 포커스 표시
|Footer의 글자와 배경간 대조가 낮음	|1.4.3 대조
|반복되는 메뉴에 대한 우회x	|2.4.1 블록 우회
|키보드 포커스 표시x	|2.4.7 포커스 표시
|이미지로 버튼 구성	|1.3.6 목적 확인


## 1. 로그인 페이지 문제 수정안
### 1. label 만들어주기
- 비장애인들은 input box 에 원하는 문구를 삽입할 수 있는 placeholder 속성을 이용해 어떤 양식의 input 인지 볼 수 있습니다. 하지만 스크린리더를 사용하는 사람들은 placeholder 속성만으로 어떤 양식의 input 인지 확인하기 어렵습니다. 따라서 label 을 꼭 달아줘야 합니다.
- design 을 위해 checkbox 를 숨겨주고 label 의 before 속성을 이용해 체크 박스를 꾸며줬습니다. checkbox 가 check 된다면 before 의 background image 를 변경해 체크 표시된 이미지를 보여주도록 해 체크 박스를 구현했습니다.
- check box 를 숨기니 tab 이 갔다는 점을 알 수 없었습니다. 이를 위해 focus 시에 border 테두리를 만들어 tab 이 정상적으로 이동했다는 점을 알려주고자 했습니다.
- 구현 후 접근성 검사시에 아래와 같은 경고문이 발생했습니다.
![image](https://user-images.githubusercontent.com/41986911/117285437-fd261b00-aea2-11eb-8387-d9c57c15277f.png)

- 이는 label 이 텍스트를 포함하지 않는다면 연결된 input 대한 정보를 사용자에게 제공하지 않기 때문에 나타나는 에러입니다. mdn 의 label 에서도 아래와 같이 명시하고 있습니다.

![image](https://user-images.githubusercontent.com/41986911/117285426-f9929400-aea2-11eb-9110-601c215b5ed8.png)

- input 의 경우 text content 가 아니기 때문에 대체 텍스트를 제공해줘야 합니다.
- 장애 등의 이유로 다른 형태로 정보를 인식하는 경우에 보조기기를 통해 원하는 형식으로 

- 이 문제를 해결하기 위해 title 속성을 label 에 의미있게 기입해주었습니다. ID 를 입력해야 한다면 "아이디 입력" 으로, PW 를 입력해야 한다면 "패스워드 입력" 으로 읽었을때 한 번에 이해가 가능하도록 기입해주었습니다.

### 2. tab 이동 확인 불가능
- 로그인 페이지에서의 아이디와 비밀번호 input 을 제외한 영역에서는 focus 를 확인할 수 없습니다. tab 키를 사용하지 않는 비장애인들은 자신이 어떤 영역을 클릭했는지에 대해 명확하게 알 수 있지만 focus 영역에 대한 표기가 없다면 2.4.7 포커스 표시 원칙을 지키지 못합니다.
- 만약 키보드 사용자가 있다면 포커스 영역을 확인할 수 있도록 포커스 표시를 제공해줘야 합니다.
- 이를 위해 :focus 속성을 사용헤 outline 을 만들어 주었습니다. 이를 통해 로그인 페이지에서 키보드 이동시에 focus 위치를 확인 가능합니다.
- 여기서 checkbox 문제가 발생했습니다. 디자인을 위해 checkbox 를 숨겨줬기 때문에 focus 가 가지 않는 문제가 발생했습니다.
- 이를 위해 input 과 label 을 감싸고 있는 div box 를 만들어주고 label focus 시에 부모 요소의 테두리가 보이도록 만들어 주었습니다. focus:within 속성을 사용했습니다.
![image](https://user-images.githubusercontent.com/41986911/117290097-5c3a5e80-aea8-11eb-97cf-d986a60c9269.png)

## 2. footer
- footer 페이지의 경우 desktop 에서 제공되는 내용들이 mobile 에서는 자세히보기 버튼 클릭시에만 노출되도록 구성되어 있습니다. 이를 위해 hidden class 를 사용해주어 display 를 none 으로 바꾸어준 후 자바스크립트를 이용해 자세히보기 클릭시에 hidden 클래스가 있는 경우에는 삭제를, 없는 경우에는 삽입을 시켜주는 방식으로 구현했습니다.


### 1. 명도대비율 문제
- footer 페이지의 경우 wcag 의 1.4.3 최소 명도 대비 조건을 충족시키지 못합니다. 텍스트 및 화상 텍스트의 시각적인 표현을 위해서는 최소한 4.5:1 이상의 명도대비율을 가져야 하지만 명도 대비율이 낮아 아래와 같이 명확하게 글이 눈에 들어오지 않습니다.
![image](https://user-images.githubusercontent.com/41986911/117293348-36af5400-aeac-11eb-86b9-58fc438d86a6.png)

- 이를 위해 글자색을 선명한 검은색으로 바꾸어 주었습니다. 훨씬 가독성이 높아지고 명확하게 눈에 들어오는 것을 확인할 수 있었고 발생했던 문제도 더 이상 나타나지 않았습니다.

![image](https://user-images.githubusercontent.com/41986911/117293084-ecc66e00-aeab-11eb-968c-47ff34f21abb.png)

![image](https://user-images.githubusercontent.com/41986911/117292987-d0c2cc80-aeab-11eb-9654-ce24b0c05181.png)

### 2. 이미지로 구성된 자세히보기
- 검사탭으로 자세히보기를 눌러보니, 자세히보기 그 자체가 img 로 구성되어 있습니다. 강의 내용에서 들어서 모두 다 아시다시피 만약 글자가 단 한글자라도 바뀌게 된다면 글자가 추가된 이미지 파일을 다시 만들어서 올려야 합니다. 이런 유지 보수 문제 때문에 이미지를 통해 자세히보기를 구현하는 것은 문제가 된다고 생각해 button 을 이용해 구현했습니다.

![image](https://user-images.githubusercontent.com/41986911/117295864-53995680-aeaf-11eb-811b-e589d7a84f74.png)

![image](https://user-images.githubusercontent.com/41986911/117295834-45e3d100-aeaf-11eb-97dd-9485c1452433.png)


![image](https://user-images.githubusercontent.com/41986911/117386014-179ed980-af21-11eb-8258-a06686a7e109.png)
![image](https://user-images.githubusercontent.com/41986911/117386159-5af94800-af21-11eb-80e7-a4ec09027624.png)

