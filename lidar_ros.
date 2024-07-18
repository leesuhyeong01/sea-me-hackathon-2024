#define RX_PIN 8
#define TX_PIN 7

#include <ros.h>
#include <std_msgs/Float32.h>
#include <DFRobot_TFmini.h>
#include <SoftwareSerial.h>

ros::NodeHandle nh;
std_msgs::Float32 distance_;
ros::Publisher distancePublisher("/distance", &distance_);

SoftwareSerial mySerial(RX_PIN, TX_PIN); // RX, TX
DFRobot_TFmini TFmini;
uint16_t distance, strength; // 거리와 강도를 담는 변수

void setup() {
  nh.initNode();
  nh.advertise(distancePublisher);
  Serial.begin(9600);
  mySerial.begin(9600);
  TFmini.begin(mySerial);
}

void loop() {
  if (TFmini.measure()) {                  // 거리와 신호의 강도를 측정합니다. 성공하면 을 반환하여 if문이 작동합니다.
    distance = TFmini.getDistance();       // 거리값을 cm단위로 불러옵니다.
    strength = TFmini.getStrength();       // 신호의 강도를 불러옵니다. 측정 대상이 넓으면 강도가 커집니다.
    
    Serial.print("Distance : ");
    Serial.print(distance);
    Serial.println(" Cm");
    Serial.println();
    
    distance_.data = distance;
    distancePublisher.publish(&distance_);
  }
  
  nh.spinOnce();
  delay(100);
}
