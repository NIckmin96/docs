# What is Driver

Driver는 OS(Operating System)과 Device가 서로 소통할 수 있도록 연결해주는 Software Component입니다.

예를 들어, 한 application이 기기로부터 데이터를 읽어오려고 할 때, application 은 OS에서 실행되는 함수를 실행시키고, OS는 driver에 들어있는 함수를 실행시킴으로서 Hardware에서 데이터를 가져올 수 있게 됩니다.  
![Driver](https://learn.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/images/whatisadriver01.png)

Device는 보통 표준 hardaware 기준에 맞춰 제작되기 때문에, 대부분의 일반적인 OS와 호환이 가능하기 때문에 Device 제작자가 반드시 Driver를 제공할 필요는 없습니다.  

또한, Driver는 반드시 Device와 직접적으로 소통하는 것은 아닐 수 있습니다.  
단일 Driver를 사용하는 것 말고도, `Driver Stack`구조를 채택하는 경우도 많기 때문에, 처음 몇개의 driver에서는 OS로부터 전달된 request를 가공하고 마지막 driver에서 직접적으로 device와 소통하는 경우도 존재합니다.  
![drive stack](https://learn.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/images/whatisadriver02.png)  
그리고 이렇게 device와 직접적으로 소통하는 driver를 `function driver`라고 하며,  
function driver전에 존재하며, 준비 작업을 수행하는 driver를 `filter driver`라고 합니다.

## Software Driver
하지만 어떤 driver는 hardware device와 아무런 관련이 없을수도 있습니다.  
예를 들어, 핵심 OS 데이터 구조에 접근이 가능한 tool을 제작한다고 할때, 이 tool을 두가지 부분으로 나눠서 구성할 수 있습니다.  
![software driver](https://learn.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/images/whatisadriver03.png)

1. User mode에서 실행되며, user interface(UI)를 제공합니다.
    - `Application`
2. Kernel mode에서 실행되며, core operating system data에 접근이 가능합니다.*(시스템 핵심 데이터)*  
    - `Software driver`

이를 정리해보자면, driver는 hardware device와 OS간의 communication이 원활히 이뤄질 수 있도록 연결해주는 software 중개자 역할이라고 할 수 있으며,  

그 외에도 OS의 핵심 데이터에 접근하도록 도와주는 software component라고 정리할 수 있을 것 같습니다.

# Reference
[What is driver](https://learn.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/what-is-a-driver-)