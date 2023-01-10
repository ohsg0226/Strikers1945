# Strikers1945

유니티를 이용하여 만들어본 간단한 2D 슈팅 게임 입니다.

## Trouble Shooting

- **Select 페이지에서 전투기를 선택 시 동일 기종을 게임 플레이 화면에서 어떻게 띄울 수 있을까?**
DataManager 파일에 static 변수를 선언하여 Select페이지에서 선택한 전투기를 다음 화면에 넘겨줌으로써 해결하였다.
"DontDestroyOnLoad"메소드를 이용하여 유니티에서 한 씬에서 다른 씬으로 넘어갈 때 기존에 있던 오브젝트들이 사라지는 것을 막아 게임 플레이 화면에 전투기 오브젝트를 넘겨주었다.
- **NullReferenceException: Object reference not set to an instance of an object**
Swift에서 메소드들이 소문자로 시작하여 "awake()"라고 선언하여 발생한 문제였다. "Awake()"메소드 안에서 변수에 값을 넣지 못해 발생한 문제였다. "Awake()"로 선언하여 해결하였다.
- **비행기가 화면 밖을 벗어나는 문제**
```
if (horizon < 0f && isTouchLeft) horizon = 0f;
if (horizon > 0f && isTouchRight) horizon = 0f;
if (vertical < 0f && isTouchBottom) vertical = 0f;
if (vertical > 0f && isTouchTop) vertical = 0f;
```
isTouchLeft와 같은 bool값으로 boxcollider에 비행기가 닿았는지, horizon과 verical의 좌표값이 화면 밖을 벗어나는지 확인하는 방식으로 해결하였다.
- **성능 관련 문제**
슈팅 게임 특성 상 적 비행기, 총알과 같은 게임 오브젝트를 계속 Destory와 Instantiate를 이용하여 생성 및 파괴하면 성능 저하가 발생하므로 오브젝트 풀링 기법을 이용하여 게임이 시작될 때 필요한 만큼 오브젝트를 생성해놓음으로써 최적화를 하였다.
- **적 비행기 무작위 생성**
적 비행기가 생성되는 위치인 spawnpoint를 미리 설정하고 spawn되는 정보를 가지고 있는 클래스를 이용하였다.
