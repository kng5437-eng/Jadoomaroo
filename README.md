# Jadoomaroo
2022/1 JBNU capston design

================================================================================


[스마트 딜리버리 로봇 코드]

1. arduino_YDLidarESP32last4.7z


-> (개인적으로 가장 힘들었던 파트, 원래 ros에서 사용할 수 있는 패키지가 있지만.. 우리팀은 esp32의 rosserial(유선x 무선o)로 연결해야하기 떄문에 아두이노 환경의 ydlidar 제어 방법을 찾아야했음.)


   esp32칩에 업로드하면 ydlidar와 RT,TX 통신하며 라이다 돌아가는 모터를 제어함
   
   
   특히 ESP32칩은 ROS MASTER와 TCP통신을 할 수 있음(하단의 ROSSERIAL_PYTHON의 노드를 통해)
   
   
   다만 아쉬운 점은, ROSSERIAL의 SENSOR_LASER_SCAN 데이터 형식을 사용하고 싶었지만, 해당 ESP32칩의 사양에 적합하지 않다는 결론을 내림(새롭게 거리 계측값만 보내는 식으로 대체했음)
   

   
2. arduino_driving.zip


-> esp32칩에 업로드하면 입력해놓은 와이파이에 연결된 후, ROS MASTER와 연결되어 topic을 subscribing할 준비를 함


   다만 아쉬운 점은, telop_twist_keyboards 노드와 연결할 때 더 다양한 제어(상황에 맞는 속도조절 등)를 시도하고 싶었지만, 
   프로젝트 시간 제약 때문에 주행속도를 고정시킨 후 간단한 상황제어만 가능하게 코드를 작성함
   
   
   (실제 geometry_twist 양식에 맞게 수정하고 싶었지만, publish하는 node를 수정할 시간이 부족하다 판단하여, 실제 필요한 상황만 분류해 간단하게 수정함)
                              -> 파일 내용을 열어보면 본래의 x,y,z,각도값 데이터 각각의 역할이 정확하게 일치하진 않음(다만 실제 주행에는 문제없음)  

3. arduino_gimbal.zip


-> esp32칩에 업로드하면 mpu6050의 값에 기반하여 서보모터를 조작하게끔 코드가 작성되어있음


   처음에는 계측값을 " digital_write( 계측값 ); "형식으로 사용하려했지만, " if문과 do while문 " 을 사용하는 것이 더 적합했음
   
   
   (mpu6050이 계측할때의 값은 트레이가 보정될때 같이 보정되어버리기때문에 순수한 계측값은 실제 보정에 유효하지 않고, 순수한 계측값의 변화량이 실제 보정에 유효했기 때문)

4. rosserial.zip


-> ros를 공부하며 가장 힘들었던 부분, 실제 esp32칩과 Ros가 Tcp통신(유선x 무선ㅇ)을 하면 된다는 점을 알아차리기까지 수많은 시행착오를 겪었음


   사용법은 rosserial_python 파일에 있는 노드 2개를 rosrun하면 됨(하나는 라이다센서용 subscribing 노드, 다른 하나는 주행부를 위한 publishing 노드)

5. teleop_twist_keyboard.zip


-> 실제 주행부를 제어하기 위한 노드가 들어있음


   (터틀봇에서 사용하는 keyboard 제어 양식에 맞춰 새롭게 수정함)  
   
   
========================================================================

(만약 본 제품과 관련하여 궁금한 사항이 있으시면 kng5437@naver.com 로 연락주시길 바랍니다.)
