---
title: GPU server 관련
author: Joonseo Hyeon
layout: post
---

서버-host-jupyter notebook-client에 대해서는 따로 연락 바람

server에서 GPU를 사용하는지 실시간으로 알 수 있는 방법은 Ubuntu kernel에서 nvidia-smi를 입력하여 점유중인 프로세스가 있는지 확인하는 것이다.

- 이외에는 다른 방법이 없어 더이상 코드를 돌리지 않으려면 커널을 shutdown하여 점유된 GPU 자원이 반납될 수 있도록 하자.

코드가 완료됐는지 확인하기 귀찮다면 이메일 발송 코드를 작성하자.
