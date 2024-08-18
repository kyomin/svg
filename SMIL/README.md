# 개요

![image](https://github.com/user-attachments/assets/22828b16-fce4-4037-861b-70f40166ccec)

위의 이미지가 GIF도 APNG도 아닌 것 같은데 움직이는 것처럼 보인다면 착각이 아니다.

# Synchronized Multimedia Integration Language

SMIL은 원래 다양한 멀티미디어 데이터를 동기화해 프레젠테이션하기 위해 타이밍, 레이아웃을 지정할 수 있는 마크업 언어이다.   
그렇기 때문에 보통 과거 `<embed>`와 외부 애플리케이션(ActiveX)을 통해 실행되는 멀티미디어를 동기화시키기 위해 사용되었으나, IE와 XML 기반 데이터와 함께 잘 사용되지 않게 되었다.

# SVG SMIL Animation

SVG SMIL Animation을 구글에 검색해보면 이미 사장(Deprecated) 되었다거나 CSS 애니메이션으로 대체된 형식이라는 주장이 가득하다.   
결론부터 말하자면 아니다.   
   
정확한 결론은 `SMIL Animation의 Deprecation이 Suspended` 된 것이다.   
즉 SMIL Animation을 사용하지 않겠다고 선언한 것을 보류했다는 뜻으로, 한동안 CSS 애니메이션과 SMIL을 같이 사용하는 것으로 결정되었다.

# SMIL Animation은 충분히 강력하다

![batman-logo](https://github.com/user-attachments/assets/75af22de-f08b-4d6b-aa79-a60f0f8ad5e1)

SVG SMIL Animation의 특징인 Path 애니메이션으로 표현한 위 역대 배트맨 로고는 단일 SVG 파일이다.   
   
CSS 애니메이션은 충분히 좋지만, SVG SMIL 애니메이션을 완벽히 대체할수는 없는 상황이다.   
몇 가지 예시를 들어보자.   
   
SMIL 애니메이션은 애초에 XML(SVG)와 함께 개발되어, 최적화되어 있다.   
CSS 애니메이션은 확실히 문서 요소에 대한 애니메이션을 적용하는 데는 부족함이 없지만, SVG는 그래픽 마크업으로서 `<defs>`의 도형 요소를 위한 보조 요소가 존재한다.   
문서 요소의 크기, 위치, 각도 등과 같은 레이아웃을 중점적으로 지원하는 CSS 애니메이션으로는 보통 SVG의 `<defs>`에서 표현되는 filter와 gradient와 같은 요소의 특성값을 변경하는 애니메이션을 지정할 수 없다.   
   
CSS 애니메이션은 HTML 요소에 대해서는 인라인 특성값을 참조하는데 문제가 없지만,
CSS 자체의 한계로 SVG 요소에서 사용되는 특성값과의 충돌을 보장할 수 없어 MDN의 SVG에 CSS 적용하기 튜토리얼에서도 하나하나 테스트해보는 수밖에 없다.   
   
SMIL 애니메이션의 특징은 SVG의 Path를 사용할 수 있다는 부분이다.   
위의 이미지들은 Path와 SMIL 애니메이션을 적용한 예시로,   
첫 번째 이미지에서는 `<mpath>`를 사용한 path 경로를 따라 움직이는 도형 그룹이 열차가 있으며,   
배트맨 로고에서는 `<path>` 내부의 `<animate>`를 통해 큐빅 베지어 패스의 기준점과 제어점을 편집했다.   
   
가장 큰 장점으로, SMIL은 원래 이름부터 Synchronized인 만큼 각 애니메이션에 대해 논리적인 연결이 가능하다.   
CSS 애니메이션을 사용해보면서 느낀 가장 큰 단점이 모든 시작, 지연 시간 기준을 절대값으로만 설정해야 한다는 것이다.   
애니메이션 키프레임 테이블을 따로 작성해두고 작업하는것 자체도 끔찍하지만, 더 큰 문제는 키프레임 수치와 애니메이션, 요소에 대한 논리적 연결성이 떨어진다는 부분이다.   
SMIL 애니메이션의 경우 `begin="anPathWalk.end"`과 같은 특성값을 통해, 다른 애니메이션 요소의 종료 시점을 통해 연속적인 애니메이션을 지정할 수 있다.