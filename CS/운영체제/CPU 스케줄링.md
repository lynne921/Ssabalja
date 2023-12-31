# CPU 스케줄링 개요

**CPU 스케줄링: 운영체제가 프로세스들에게 CPU 자원을 배분하는 것**

## 프로세스 우선순위

- 입출력 집중 프로세스(I/O bound process): 입출력 버스트(I/O burst)가 많은 프로세스
- CPU 집중 프로세스(CPU bound process): CPU 버스트(CPU burst)가 많은 프로세스

입출력 집중 프로세스를 가능한 빨리 실행시켜 입출력장치를 작동시키고 CPU 집중 프로세스에 집중적으로 CPU를 할당하는 것이 더 효율적이다.

**우선순위**

운영체제는 각 PCB에 우선순위를 명시하고, PCB에 적힌 우선순위를 기준으로 먼저 처리할 프로세스를 결정한다.

## 스케줄링 큐(scheduling queue)

특정 입출력장치를 사용하고 싶은 프로세스들을 모두 줄 세우는 방법. 운영체제가 관리하는 대부분의 자원은 큐로 관리된다.
<img width="80%" src="https://github.com/lynne921/Ssabalja/assets/96831825/a3db4fde-5a82-4809-96a1-98fdb728f928"/>


준비 큐는 CPU를 이용하기 위해 기다리는 줄이고, 대기 큐는 입출력장치를 이용하기 위해 기다리는 줄

먼저 큐에 삽입되었어도 높은 우선순위를 가진 프로세스가 먼저 실행된다.
<img width="80%" src="https://github.com/lynne921/Ssabalja/assets/96831825/9a49244a-90d1-49df-b86b-715c3db21765"/>

## 선점형과 비선점형 스케줄링

**선점형 스케줄링(preemptive scheduling)**

프로세스가 CPU를 비롯한 자원을 사용하고 있더라도 운영체제가 프로세스로부터 자원을 강제로 빼앗아 다른 프로세스에 할당할 수 있는 스케줄링 방식

→ 어느 하나의 프로세스가 자원 사용을 독점할 수 없음.

→ 문맥 교환 과정에서 오버헤드가 발생할 수 있음.

**비선점형 스케줄링(non-preemptive scheduling)**

하나의 프로세스가 자원을 사용하고 있다면 그 프로세스가 종료되거나 스스로 대기 상태에 접어들기 전까진 다른 프로세스가 끼어들 수 없는 스케줄링 방식

→ 하나의 프로세스가 자원 사용을 독점할 수 있음.

→ 모든 프로세스가 골고루 자원을 사용할 수 없다는 단점

# CPU 스케줄링 알고리즘

## 스케줄링 알고리즘의 종류

1. 선입 선처리 스케줄링(FCFS 스케줄링)
    
    단순히 준비 큐에 삽입된 순서대로 프로세스들을 처리하는 비선점형 스케줄링 방식
    
    호위 효과(2ms를 실행하기 위해 22ms라는 긴 시간을 기다려야함)
    
2. 최단 작업 우선 스케줄링
    
    준비 큐에 삽입된 프로세스들 중 CPU 이용 시간의 길이가 가장 짧은 프로세스부터 실행하는 스케줄링 방식. 최단 작업 우선 스케줄링(SJF 스케줄링)이라고 한다.
    
    기본적으로 비선점형 스케줄링 알고리즘으로 분류되지만 선점형으로 구현될 수도 있다.
    
3. 라운드 로빈 스케줄링
    
    선입 선처리 스케줄링 + 타임 슬라이스
    
    ***타임 슬라이스***
    
    : 각 프로세스가 CPU를 사용할 수 있는 정해진 시간
    
    선점형 스케줄링이다.
    
    라운드 로빈 스케줄링에서는 타임 슬라이스 크기가 매우 중요하다.
    
4. 최소 잔여 시간 우선 스케줄링(SRT 스케줄링)
    
    최단 작업 우선 스케줄링 알고리즘과 라운드 로빈 알고리즘을 합친 스케줄링 방식
    
    선점형 스케줄링 알고리즘
    
    최소 잔여 시간 우선 스케줄링 하에서 프로세스들은 정해진 타임 슬라이스만큼 CPU를 사용하되,  CPU를 사용할 다음 프로세스로는 남아있는 작업 시간이 가장 적은 프로세스가 선택된다.
    
5. 우선순위 스케줄링
    
    프로세스들에 우선순위를 부여하고, 가장 높은 우선순위를 가진 프로세스부터 실행하는 스케줄링 알고리즘(우선순위가 같다면 선입 선처리로 스케줄링)
    
    우선순위가 높은 프로세스가 계속 먼저 실행되어 우선순위가 낮은 프로세스는 실행이 연기되는 **기아 현상**이 생길 수 있음
    
    ***에이징***: 오래 대기한 프로세스의 우선순위를 점차 높이는 방식
    
6. 다단계 큐 스케줄링
    
    우선순위별로 준비 큐를 여러개 사용하는 스케줄링 방식
    
    프로세스 유형별로 우선순위를 구분하여 실행하는 것이 편리해진다.
    
7. 다단계 피드백 큐 스케줄링
    
    다단계 큐 스케줄링에서 발생할 수 있는 기아 현상을 방지할 수 있는 스케줄링 알고리즘
    
    프로세스들이 큐 사이를 이동할 수 있기 때문에 에이징 기법을 적용할 수 있다.

   프로세스의 CPU 이용 시간이 길면 낮은 우선순위 큐로 이동시키고, 낮은 우선순위 큐에서 너무 오래 기다린다면 높은 우선순위 큐로 이동시킨다.

<img width="80%" src="https://github.com/lynne921/Ssabalja/assets/96831825/eb07e14e-45bf-41d7-a944-07708f5c8f13"/>
