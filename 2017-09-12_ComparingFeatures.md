## Feature Descriptors
#### SIFT
* local feature 들은 스케일, 회전, 밝기변화에 불변 특징을 위해 구분력을 희생하므로, 하나의 특징점에 수많은 특징점 매칭 가능
* feature 자체의 성능보다 어떤 매칭 방법을 사용했느냐에 따라 최종 성능 좌우 가능

#### Ferns
*  밝기차의 부호 정보만을 이용하기 때문에 영상의 contrast 변화, 밝기 변화 등에 강인

#### HOG
* HOG는 템플릿 매칭과 히스토그램 매칭의 중간 단계에 있는 매칭 방법으로 볼 수 있으며 블록 단위로는 기하학적 정보를 유지하되, 각 블록 내부에서는 히스토그램을 사용함으로써 로컬한 변화에는 어느정도 강인
* HOG는 물체의 실루엣(윤곽선) 정보를 이용하므로 사람, 자동차 등과 같이 내부 패턴이 복잡하지 않으면서도 고유의 독특한 윤곽선 정보를 갖는 물체를 식별하는데 적합한 영상 feature

#### Haar
* 물체의 기하학적 정보를 유지하며 영역 단위의 밝기차를 이용하기 때문에 영역 내부에서의 물체의 형태변화 및 약간의 위치변화를 어느정도 커버할 수 있는 특성을 갖는다. 하지만 **영상의 contrast 변화, 광원의 방향 변화에 따른 영상 밝기 변화에 영향**을 받으며 물체가 **회전된 경우**에는 검출이 힘들다.

#### LBP
* 텍스쳐에 대한 패턴 정보 저장

#### MCT
![MCT](http://cfile9.uf.tistory.com/image/2435A84C52CE4E1A2B17BC)
* 조명 변화에 따른 차이가 제거되고 물체의 패턴 정보만 남음
* LBP 와 유사

## Features 비교
#### Haar/LBP vs. HOG
* Haar and LBP
  * fine-scale texture 에 적합 -> 얼굴인식 등에 사용 ([1](http://kr.mathworks.com/help/vision/ug/train-a-cascade-object-detector.html?requestedDomain=kr.mathworks.com#btu4e5l-1))

* HOG
  * 전체적인 shape/실루엣 저장 -> 사람 인식 / 자동차 인식 등에 사용 ([1](http://kr.mathworks.com/help/vision/ug/train-a-cascade-object-detector.html?requestedDomain=kr.mathworks.com#btu4e5l-1))

#### SIFT vs. HOG ([2](http://darkpgmr.tistory.com/116))
  * HOG
    * 일종의 템플릿 매칭
    * 물체가 회전된 경우나 형태변화가 심한 경우에는 검출이 어려움
  * SIFT
    * 모델의 특징점과 입력 영상의 특징점에 대해 특징점 단위로 매칭이 이루어짐
    * 물체의 형태변화, 크기변화, 회전 등에 강인
  * HOG는 물체의 형태변화가 심하지 않고 **내부 패턴이 단순**하며 **물체의 윤곽선으로 물체를 식별할 수 있을 경우**에 적합하고 SIFT는 액자 그림과 같이 **내부 패턴이 복잡하여 특징점이 풍부한 경우**에 적합한 방법이다.

#### Haar vs. Ferns
* Haar
  * **영역 단위**의 밝기차를 이용
  * 밝기차에 대한 실수값 이용
* Ferns
  * **픽셀 단위**의 밝기차를 이용
  * 밝기차에 대한 부호 이용

#### SIFT vs. Ferns
* SIFT
  * Local patch 에 대한 밝기 히스토그램
* Ferns
  * Local patch 에 대한 밝기 템플릿
  * 형태 변화나 회전에 취약 => 학습 시 미리 변형하여 학습데이터 생성
  * Offline 학습 필요함

#### Haar vs. LBP
* LBP
  * Haar 와 유사한 특성
  * 좀 더 세밀한 패턴 변화 표현 가능
