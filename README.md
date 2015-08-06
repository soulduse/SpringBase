# SpringBase
스프링 베이스 프로젝트

5. debugging 사용정리
=========================

정의 
--------------------------------
  - 버그 : 프로그램에서 발생하는 오류.
  - 디버깅 : 프로그램에 발생하는 오류를 수정 하는 것.

사용법
--------------------------------
  - Debug Perspective 상태로 접근하기 위해서는
    Window -> Open Perspective -> Debug를 선택 또는,
    오른쪽 위에 있는 Perspective toolbar 아이콘으로 변경가능.
  - 소스코드 레벨의 디버그가 가능하여 Step, Into, Step Over, Step Return 기능으로 한줄 또는 블럭별로 실행이 가능하다.
  - 소스코드 왼쪽의 여백을 더블클릭 하면 breakpoint 토클 설정도 가능하다.

![Debug_IMG01](http://cafeptthumb3.phinf.naver.net/20150806_130/soulduse_1438821825576Mba7w_PNG/debug001.PNG?type=w740)

![Debug_IMG02](http://cafeptthumb2.phinf.naver.net/20150806_100/soulduse_14388218257078TIGg_PNG/debug002.PNG?type=w740)

![Debug_IMG03](http://cafeptthumb1.phinf.naver.net/20150806_158/soulduse_1438821825786XrJQc_PNG/debug003.PNG?type=w740)

![Debug_IMG04](http://cafeptthumb3.phinf.naver.net/20150806_296/soulduse_1438821825867VGpye_PNG/debug004.PNG?type=w740)

[소스코드 URL](https://bitbucket.org/koolsign/code.android.base/src/c9b00ee5c05ed4e531c4d86751e2ada356b95f06/DebugTest/?at=khw.code)



6. junitTest	
=========================

정의 
--------------------------------
  
  * JUnit
  > 단위 테스트를 위한 프레임워크
  > JUnit은 테스트 주도 개발(TDD, Test-Driven Development, 테스트를 먼저 한 뒤 코드를 작성하는 방법)에서
    많이 사용하는 프레임워크이며 자동화된 테스트가 가능.

  * 단위테스트란? 
  > 테스트 대상이 되는 코드 기능의 아주 작은 특정 영역을 실행해 보는, 개발자가 작성한 코드 조각이다.
	대개 단위 테스트는 특정 상황에서 특정 메서드를 실험해 본다. 이는 어떤 코드 조각이 개발자가 생각한 대로 동작하는지 증명하기 위해 수행하는 것이다.
  
  * 왜 귀찮게 단위 테스트를 해야 하는가?
  > 설계를 좀더 좋게 만들어주고, 디버깅에 낭비하던 시간을 줄여준다.

사용법
--------------------------------
- 이클립스에서 단위 테스트 방식에는 두 가지 방식이 있다.
  (테스트 프로젝트 만드는 방식 / 이미 있는 프로젝트에서 단위테스트 하는 방식)

  [이미 있는 프로젝트에서의 단위테스트]
  1. 프로젝트 오른쪽 클릭 > New > JUnit Test Case 생성

  ![JUnit_IMG_001](http://cafeptthumb3.phinf.naver.net/20150806_224/soulduse_1438837217855RkDrY_PNG/JUnit004.PNG?type=w740)
  
  2. 아래와 같은 구성이 된다.
  
  ![JUnit_IMG_002](http://cafeptthumb1.phinf.naver.net/20150806_244/soulduse_1438837217694oyxKx_PNG/JUnit002.PNG?type=w740)
  
  3. 단위테스트 할 클래스를 아래의 소스와 같이 작성한다.

- 테스트 대상 프로젝트 HelloWorldActivity.class
```
public class HelloWorldActivity extends Activity {
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        plus();
    }
    
    public int plus(){
    	int i = 1;
    	int j = 2;
    	int k = i+j;
    	
    	return k;
    }
}

```

- 테스트 프로젝트 HelloWorldActivityTest.class
``` HelloWorldActivity.class
public class HelloWorldActivityTest extends ActivityInstrumentationTestCase2<HelloWorldActivity> {
	
	// 생성자 필수
	public HelloWorldActivityTest(){
		super(HelloWorldActivity.class);
	}
	
	// 테스트 대상 액티비티
	HelloWorldActivity activity;

	protected void setUp() throws Exception {
		super.setUp();
		activity = getActivity();
	}

	protected void tearDown() throws Exception {
		super.tearDown();
	}
	
	// public 이며 함수명이 test{Xxx}로 시작하는 암수를 테스트한다.
	
	// 테스트 실패 함수 
	public void testFail(){
		Log.d("fail!", "fail!");
		fail("check Android JUnit Env. Setup");
	}
	
	// 테스트 성공 함수
	public void testTrue(){
		Log.d("success!", "success!");
		assertTrue(true);
	}
	
	// 대상 액티비티에서 함수를 불러와서 테스트
	public void testPlus(){
		int i = 3;
		int a = activity.plus();
		assertEquals(i, a);
	}
}
```
  4. 실행방법은 Run -> Run As -> Android JUnit Test
  5. 실행결과 단위별 테스트가 가능하다.

  ![JUnit_IMG_003](http://cafeptthumb1.phinf.naver.net/20150806_223/soulduse_14388377475415qNuU_PNG/JUnit005.PNG?type=w740)

JUnit 프레임워크의 유용한 클래스들 _ Assert class
--------------------------------

![JUnit_IMG_004](http://cafeptthumb1.phinf.naver.net/20150806_128/soulduse_1438837217588vc8R7_PNG/JUnit001.PNG?type=w740)
