# Chapter 2 - The Production Environment at Google, from the Viewpoint of an SRE

## Hardware

서버 하드웨어와 서버 소프트웨어 단어 간 의미의 모호함을 해소하기 위해서, 실제 물리적인 하드웨어+VM은 Machine이라고 정의하고 서비스를 구현하는 소프트웨어는 Server라고 정의.  
=> 이렇게 정의를 하는 것이 매우 옳다고 생각하며 이전 문서와 앞으로의 문서에서 반영 중임.

Google의 데이터 센터는 수십대의 Machine을 가진 Rack > Rack들을 묶어 Cluster를 구성.

## Software that coordinates the hardware

한 해 동안 발생하는 머신/디스크 문제를 해소하기 위해 추상화로 해결을 하려고 시도 => Borg (Kubernetes의 전신)

Borg Master => Control Plane
Borglet => Kubelet

BNS (Borg Naming Service) => Kubernetes의 Service와 원리가 매우 유사 (`/bns/<cluster>/<user>/<job>/<task>`)  
Borg Task의 restart => Pod나 Container의 restart와 유사 (일단 서비스의 유지가 우선이라는 관점)

## Software Infrastructure

Backend는 Server, Frontend는 Client로 과거에는 구분을 했었다고 말하는데, 다시 Server/Client로 구분을 하는 것이 맞다고 생각.  
웹서비스 개발자들이 많아지면서 Backend/Frontend가 고유명사처럼 되어버렸지만, 기존 여러 소프트웨어 추상화 구분 등을 고려하면 Server/Client로 명확하게 정의하는 것이 맞는 듯.
