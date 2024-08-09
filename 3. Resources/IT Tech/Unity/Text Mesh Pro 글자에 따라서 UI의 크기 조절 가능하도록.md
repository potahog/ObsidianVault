```
private TMP_Text text; (or Text text)

...
private void SetTextSize(text message){
	text.text = message;
	var preferredSize = text.GetPreferredValues(message);
}

``` C#

UGUI의 Text 혹은 TMP_Text(Unity 2022버전부터 공식적으로 기본 Text UI Element로 지정됨.)에 포함된 Method 중 하나인 GetPreferredValues 를 활용하면 string 크기에 따른 UI Size를 얻을 수 있다. (정확히는 string이 ugui에서 사용할 크기)