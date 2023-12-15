DL 프로젝트를 하다보면, CUDA에 대해서 한번 쯤은 들어보신적이 있으실겁니다.  

저 역시, CUDA에 대해서 많이 들어보기는 했지만 CUDA가 정확히 무엇이고 왜 중요한지에 대해 잘 알지 못했는데 최근 CUDA관련 이슈로 인해서 고생을 좀 하다보니 정리해 봐야겠다는 생각이 들었습니다.

# Reference
[What is CUDA](https://blogs.nvidia.com/blog/what-is-cuda-2/)  
[About-cuda](https://developer.nvidia.com/about-cuda)  
[An Easy Introduction to CUDA C and C++](https://developer.nvidia.com/blog/easy-introduction-cuda-c-and-c/)  
[An even easier Introduction to CUDA](https://developer.nvidia.com/blog/even-easier-introduction-cuda/)  
[CUDA - wiki](https://ko.wikipedia.org/wiki/CUDA)

# CUDA의 주 목적
CUDA는 NVIDIA에서 개발한 parallel computing platform이자 programming model이며, CUDA를 사용함으로서, GPU에서 병렬 처리 연산을 가능하게 도와줍니다.

# CUDA Programming model basics
CUDA programming model은 CPU와 GPU모두를 사용하는 모델입니다. CUDA에서, `host는 CPU`를 참조하고 `device는 GPU`를 참조하게 됩니다.  
host에서 실행되는 코드는 host, device 모두의 메모리를 관리할 수 있으며, 