---
layout: entry
title: 비트맵 방식과 벡터 방식
author: 최재형
author-email: monday@spoqa.com
description: 컴퓨터를 이용한 그래픽 디자인의 정말 기본이 되는 이미지 형식에 대해 다루어 보겠습니다.
publish: true
---

안녕하세요? 스포카에서 디자인 총괄을 맡고있는 최재형입니다. 저는 스포카 기술 블로그에서 그래픽 디자인에 대한 기본적인 내용을을 다루어 볼까 합니다. 

앞으로 저는 컴퓨터 그래픽 디자인의 기초적인 용어 정리 및 개념 설명부터 실무에 바로 도움이 되는 디자인의 기본 상식 및 방법론까지 스포카 기술 블로그를 통해 설명해 보고자 합니다. 일단 오늘은 컴퓨터를 이용한 그래픽 디자인의 정말 기본이 되는 이미지 형식에 대해 다루어 보겠습니다.

비트맵<sub>Bitmap</sub> 방식과 벡터<sub>Vector</sub> 방식
---
일단 컴퓨터 그래픽은 크게 비트맵<sub>Bitmap</sub>과 벡터<sub>Vector</sub>방식으로 구분됩니다. 비트맵<sub>Bitmap</sub>은 ‘비트의 지도<sub>map of bits</sub>'란 듯으로, 각 픽셀에 저장된 일련의 비트 정보 집합이라고 보시면 됩니다. 디스플레이는 픽셀들의 배열로 구성되어 있습니다. 픽셀들의 배열 방식, 픽셀들의 총 숫자나 가로 세로의 비율이 그 디스플레이의 해상도를 결정짓습니다. 예를들어 1920 x 1080의 해상도를 가진 디스플레이는 가로 1920개, 세로 1080개의 픽셀들을 가진 다는 것을 의미합니다. 가로와 세로의 값을 곱하면 그 디스플레이가 가진 총 픽셀 수가 됩니다.

![1_Pixel](/images/bitmap-vector/1_Pixel.png)

하나의 픽셀은 R<sub>빨강</sub>, G<sub>초록</sub>, B<sub>파랑</sub>의 세 가지의 서브 픽셀<sub>subpixel</sub>로 이루어져 있습니다, 서브 픽셀의 배열 방식은 디스플레이의 특성에 따라 모두 다릅니다. 서브 픽셀의 배열 방식의 차이는 너무 깊은 얘기이니 본편에서는 다루지 않기로 하겠습니다. 참고로 보편적으로 가장 많이 쓰이고 있는 LCD 방식은 그림에서와 같이 RGB가 하나의 픽셀을 이루어 전체 디스플레이에 배열이 연속됩니다. 

각 픽셀의 R, G, B는 0~255까지의 값을 가지고 있는데, 이 셋의 조합 (R,G,B)이 그 픽셀의 색상을 정의하게 됩니다. 그리고 그 정의된 색상들의 픽셀이 모여 지도<sub>map</sub>를 만들게 되고, 하나의 이미지 파일을 만들게 됩니다. (참고로 RGB로 색을 표현하는 방식인 RGB 가산혼합의 메커니즘은 다음 문서 <sub>http://ko.wikipedia.org/wiki/RGB</sub> 를 참조하시길 바랍니다.) 

![2_Rasterize.png](/images/bitmap-vector/2_Rasterize.png)

비트맵<sub>bitmap</sub>은 다른 표현으로 픽스맵<sub>pixmap</sub>이나 래스터<sub>raster</sub> 이미지로도 불립니다. 포토샵에서 벡터 기반의 레이어 오브젝트 - 예를 들면 벡터 오브젝트나 편집 가능한 상태의 글자 - 를 비트맵화 시키는 메뉴 이름이 ‘Rasterize Layer’인데, 아마 여기에서 많이 보셨을 단어일 겁니다.

벡터<sub>Vector</sub> 방식은 비트맵과는 반대로 표현되는 그래픽의 형태<sub>shape</sub>들이 수학적 공식으로 이루어져 있습니다. 다시말해 벡터 방식의 그래픽은 고정된 비트맵을 가지고 있는 것이 아니라,  수학적 공식으로 이루어진 오브젝트들이 그때그때 디스플레이에 비트맵화 되어 스크린에 표시됩니다. 여기에서 좀 더 높은 퀄리티의 이미지를 만들기 위해 안티-앨리어싱<sub>anti-aliasing</sub>이라는 기술이 사용되는데, 이 부분은 추후에 더 다루기로 하겠습니다.

![3_VectorComponents.png](/images/bitmap-vector/3_VectorComponents.png)

벡터 방식의 그래픽은 다음과 같은 메커니즘으로 구성됩니다. 일단 두 개의 점<sub>point</sub>이 연결되면 하나의 선<sub>path</sub>이 됩니다. 그리고 그 선<sub>path</sub>이 세 개 이상이 되면 면을 만들 수 있습니다. 그리고 각각의 선은 두께 값과 색상 값, 곡률 값을, 면은 색상 값을 가질 수 있습니다. 이렇게 점과 선, 면의 기본적 벡터 그래픽 요소들이 모여 다양하고 복잡한 벡터 그래픽을 만들 수 있게 됩니다.

비트맵 방식의 장단점
---
비트맵은 최하위의 레벨에서 렌더링 된 고정된 형식의 이미지 포맷으로, 컴퓨터에서 해당 형식의 파일을 연산하는데 많은 효율성을 지니고 있습니다. 같은 형태의 벡터 포맷 그래픽이라면 컴퓨터에서 더 많은 연산을 수행하게 되어 하드웨어에 부담을 줍니다. 그래서 대부분의 웹사이트와 어플리케이션에서는 비트맵 이미지 기반으로 구성되어 있습니다. 하지만 최근 하드웨어의 발전으로 부담이 적어져 몇몇 사이트에서는 벡터 포맷의 이미지를 실험적으로 사용하기도 합니다.

![4_QualityLoss.png](/images/bitmap-vector/4_QualityLoss.png)

<sub>http://www.cambridgeincolour.com/tutorials/image-interpolation.htm</sub>

비트맵은 최종적으로 렌더링 된 상태의 포맷이기 때문에 이미지 편집이 자유롭지 못 합니다. 그리고 해상도가 고정되어 있기에 업-스케일<sub>up-scale</sub>을 하면 퀄리티에 큰 훼손이 가며, 다운-스케일<sub>down-scale</sub>이나 회전 등의 변형 시에도 안티-앨리어싱 작업이 중복으로 적용되게 되어 이미지 퀄리티에 큰 손상이 갑니다.

비트맵 이미지의 편집 툴로는 대표적으로 Adobe Photoshop이 쓰이고 있습니다. Photoshop은 현재 GUI 작업에 가장 많이 쓰이고 있습니다. Photoshop은 Drop Shadow나 Inner Shadow, Emboss 등의 Effect 효과의 퀄리티가 가장 좋기 때문에 애플과 같은 스큐어모프<sub>skeuomorph</sub>한 장식적인 GUI를 제작하기에 가장 효과적인 툴입니다. 스큐어모프<sub>skeuomorph (http://en.wikipedia.org/wiki/Skeuomorph)</sub>라는 개념은 나중에 한 번 기회를 내서 소개해 드리겠습니다.

하지만 Photoshop은 많은 단점을 가지고 있습니다. 일단 레이어 기반의 이미지 편집 툴이기 때문에 작업하는 그래픽 오브젝트가 많아지면 레이어 관리가 정말 어려워집니다. 물론 레이어 네이밍과 컬러 태그 등을 통한 체계적인 레이어 관리로 어느정도 보완을 할 수 는 있지만, 이를 지키기는 정말 어렵습니다. 그리고 레이어를 관리하거나 찾고 편집하는 과정이 비직관적이어서 벡터 기반의 툴인 Illustrator에 비해 많은 노동 비용이 소모됩니다. 

![5a_layer.png](/images/bitmap-vector/5a_layer.png)
![5b_layer.png](/images/bitmap-vector/5b_layer.png)

또한 Photoshop은 Adobe의 프로그램 설계 의도가 그래픽 디자인 툴이 아닌 사진 편집 툴이기에 메트릭 체계를 다루기가 상대적으로 좋지 않습니다. 그래서 좌표나 크기<sub>dimension</sub> 기반의 디자인 작업을 하기에 비직관적인 면이 있습니다. 또한 Photoshop은 가이드의 기능이 부실하여 그래픽 디자인의 기본이라 할 수 있는 그리드 시스템을 운용하는데 있어서도 Illustrator에 비해 많은 단점을 가지고 있습니다.

벡터 방식의 장단점
---
벡터 포맷의 그래픽 편집 툴의 장점은 우선적으로 작업의 용이성을 들 수 있습니다. 벡터 그래픽은 점과, 점으로 이루어진 선, 면으로 모든 그래픽 요소들이 이루어져 있기에, 간단하게 점과 선을 수정하는 과정으로 그래픽 작업을 유지 관리하기가 정말 좋습니다. 즉, 벡터 포맷의 작업 파일이 보존되는 한 자유로운 수정이 가능합니다. 또한 작업된 벡터 그래픽을 바탕으로 언제든지 다양한 방식, 그리고 원하는 해상도의 비트맵 포맷으로 산출이 가능합니다.

벡터 방식의 그래픽 편집 툴은 Adobe Illustrator와 InDesign이 많이 쓰이고 있습니다. 전자는 보통의 그래픽 디자인 작업이 목적일 때, 후자는 문서 편집과 간단한 프레젠테이션이 목적일 때 주로 많이 쓰이고 있습니다. 여기서는 GUI 디자인과 그래픽 디자인에 자주 쓰이는 Illustrator의 장단점에 좀 더 집중해 보겠습니다.

Illustrator는 위에서 얘기한 벡터 포맷의 그래픽 편집 툴이 기본적으로 가지고 있는 장점 외에도 여러가지 추가적인 장점이 있습니다. 첫째로 Illustrator는 객체 지향의 편집 툴이라 복잡한 레이어 관리가 필요 없습니다. 디스플레이에 표시되는 오브젝트를 보이는 대로 선택하고 바로 편집을 할 수 있습니다. 그리고 오브젝트의 위계 관리는 포토샵의 레이어 판넬처럼 리스트 상에서 전역적으로 관리하기 보다는 오브젝트의 Arrange 기능을 이용해 상대적으로 위계를 손쉽게 관리할 수 있습니다. 또 Lock 기능과 Group 기능을 활용하여 가려져서 보여지지 않는 오브젝트를 적은 과정을 통해 효율적으로 관리할 수 있습니다.

둘째로 밀리미터 및 픽셀기반의 좌표 체계를 기반으로 작업하기가 정말 편합니다. Illustrator는 포토샵과 달리 오브젝트를 선택하면 해당 오브젝트의 좌표와 크기<sub>dimension</sub>가 모두 바로 표시됩니다. 이러한 특성들은 디자인을 코드로 구현할 때 오브젝트를 선택하기만 해도 모든 정보가 나오기 때문에 개발 작업 시 매우 용이합니다.

![6_metric.png](/images/bitmap-vector/6_metric.png)

셋째로 가이드<sub>guide</sub> 기능을 통해 효과적으로 그리드 시스템을 운용할 수 있습니다. 기본적으로 Illustrator에서의 가이드는 오브젝트와 동일 취급이 됩니다. 그렇기 때문에 가이드를 쉽게 복제 및 이동하여 다른 캔버스 및 파일로 이동하여 사용할 수 있습니다. 또한 정확하게 가이드의 위치 좌표 값을 설정 가능하기에 보다 확실하게 그리드 시스템을 운용할 수 있습니다.

Photoshop vs Illustrator
---
Photoshop과 Illustrator에는 각각의 장단점이 있습니다. 포토샵은 퀄리티가 높은 장식예술을 하기에 좋은 도구고, 일러스트레이터는 좀 더 본격적인 의미의 ‘디자인’을 하는데에 어울리는 도구입니다. 결국 디자인 과정에 있어 각 태스크의 성격에 맞는 적절한 툴을 그때그때 골라 쓰는게 가장 현명하다고 볼 수 있습니다.