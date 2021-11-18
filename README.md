# 프로젝트명

recycling box

# 프로젝트 팀 구성원

- 우경희(pm)

- 조종혁

- 윤현

# 프로젝트 개요

- 전세계적으로 회자되고 있는 환경호보, 이를 위해선 무엇보다 환경보호에 대한 관심이 우선적으로 필요하다고 생각합니다. 따라서 사람들에게 환경보호의 관심을 이끌수도 있고 흥미를 느낄수도 있을 방법을 찾던중, 만약 분리수거를 알아서 해주는 로봇이 어떨까해서 recycling box라는 주제를 선택하게 되었습니다.

- 이 recycling box의 주요 기능은 객체 인식을 통하여 분리수거가 가능한지 페트병인지, 캔인지 구분할 수 있는 기능이 있고, 부가적인 기능은 recycling box 가 꽉차있을때 fcm push 메시지를 전송하여 관리자가 확인할수 있도록 구성하였습니다. 

# HW 구성

- jetson nano board

- AVR칩을 탑재한 보드


# SW 구성

- project main func

  - pet object : matchTemplate

  - can object : masking -> findcontour -> minAreaRect & approxPolyDP 

  - find label : masking -> morphology ->labeling

  - define filepath : filesystem

- project sub func

  - push alarm : android studio and fcn

- firmware
  
  - control servo
    
  - ultrasonic 
  
  - buzzer
  
  - neo_pixel

- communitation
  
  - serial communication cpp system headers
    
  - server : nodejs
  
# 프로젝트 작업 과정

- 프로젝트 주제 정하기

- 프로젝트 기능 정하기

- 프로젝트 파트리스트 정하기

- main 기능 구현하기

- 부가 기능 구현하기


# 동작영상

opencv를 활용한 재활용 가능 pet,can 구분 구현 영상 (이미지 클릭후 영상으로 이동)
<br/>
[![Video Label](https://i9.ytimg.com/vi/2ykl-l5aJDE/mq2.jpg?sqp=CPy914wG&rs=AOn4CLDXHMoVdWipfiKss9ZlwRvxZ2FuOQ)](https://youtu.be/2ykl-l5aJDE)

recycling box 구현 영상 (이미지 클릭후 영상으로 이동)
<br/>
[![Video Label](https://i9.ytimg.com/vi/o9Qvf0xHIZE/mq2.jpg?sqp=CLiR14wG&rs=AOn4CLDapwOsRt7ClSlYkKbxjnRKmMBPaw)](https://youtu.be/o9Qvf0xHIZE)


# 코드 리뷰
### matchTemplate

![1](https://user-images.githubusercontent.com/88933098/142357606-de9da55c-f217-4e12-8ecc-d00a86a5258c.JPG)

~~~
//읽어온 이미지와 datasheet sample image를 비교하는 부분
for(int i = 0; i < SAMPLENUM; i++){
  matchTemplate(subImg_, matReadVector[i], resVecotr[i], TM_CCOEFF_NORMED);
	normalize(resVecotr[i], res_normVector[i], 0, 255, NORM_MINMAX, CV_8U);
	minMaxLoc(resVecotr[i], 0, &maxvVector[i], 0, &maxlocVector[i]);
	}
//유사도를 비교하는 부분
if(maxvVector[0] > 0.7){
	serialPort1.Write("N");
	cout << "CAP" <<endl;
	break;
}
 ~~~
 
![2](https://user-images.githubusercontent.com/88933098/142357629-9b73971e-ac28-4ed7-aae2-8cadf01b4fee.JPG)

![3](https://user-images.githubusercontent.com/88933098/142357693-31035f8c-ff64-4e6f-b780-003b7c016580.JPG)
