# Servlet-Jsp


# chap 08-2_인터페이스 타입 변환과 다형성

[개념정리](https://www.notion.so/932ff1358f6d4fa585500a60e79bdc9b)

## 자동 타입 변환

구현 객체가 인터페이스 타입으로 변환되는 것은 자동 타입 변환에 해당한다.

프로그램 실행 도중에 자동타입 변환이 일어난다.

## 필드의 다형성

7장에서는 타이어 클래스 타입에 한국 타이어와 금호 타이어라는 

자식 객체를 대입해서 교체할 수 있음을 보여주었지만

다음 그림은 타이어가 클래스 타입이 아니고 인터페이스 타입이라는 점과 

한국 타이어와 금호 타이어는 자식 클래스가 아니라 구현클래스라는 차이점이 있다.

한국타이어와 금호타이어는 공통적으로 타이어 인터페이스를 구현했기 때문에

모두 타이어 인터페이스에 있는 메소드를 가지고 있다.

따라서 타이어 인터페이스로 동일하게 사용할 수 있는 교체 가능한 객체에 해당한다.

자동차를 설계할 때 다음과 같이 필드 타입으로 타이어 인터페이스를 선언하면

필드값으로 한국 타이어 또는 금호 타이어 객체를 대입할 수 있습니다.

자동 타입 변환이 일어나기 때문에 아무런 문제가 없다.

```java
public class Car {
	Tire frontLeftTire = new HankookTire();
	Tire frontRightTire = new HankookTire();
	Tire backLeftTire = new HankookTire();
	Tire backRightTire = new HankookTire();

}
```

Car 객체를 생성한 후 초기값으로 대입한 구혀 객체 대신 다른 구현객체를 대입할 수도 있다.

이것이 타이어 교체에 해당한다.

```java
Car myCar = new Car();
myCar.frontLeftTire = new KumhoTire();
myCar.frontRightTire= new KumhoTire();
```

frontLeftTire frontRightTire 에 어떠한 타이어 구현 객체가 저장되어도  

Car  객체는 타이어 이터페이스에 선언된 메소드만 사용하므로 전혀 문제가 되지 않는다.
다음 Car 객체의 run() 메소드에서 타이어 인터페이스에 선언된  roll() 메소드를 호출한다.

```java
void run() {
	frontLeftTire.roll();
	frontRightTire.roll();
	backLeftTire.roll();
	backRightTire.roll();

}
```

frontLeftTire frontRightTire 교체하기 전에는 HankookTire 객체의 roll() 메소드가 호출되지만

KumhoTire  로 교체된 후에는 KumhoTire 객체의 roll() 메소드가 호출됩니다.

Car 의 run()  메소드를 수정하지 않아도 

다양한 roll() 메소드의 실행결과를 얻을수 있게 되는 것입니다.

이게 바로 필드의 다형성

 소스예제

```java
package ch8_2;

public interface Tire {  //Tire 라는 인터페이스를 가지고 호출할수 있는 메소드가 바로 roll()
	public void roll();  //roll() 메소드 호출방법 설명
	
}
```

```java
package ch8_2;

//구현클래스
public class HankookTire implements Tire{
	
	//Tire 인터페이스 구현
	@Override
	public void roll() {
		System.out.println("한국 타이어가 굴러갑니다.");
	}
	
}
```

```java
package ch8_2;

//구현클레스
public class KumhoTire implements Tire {
	
	//Tire 인터페이스 구현
	@Override 
	public void roll() {
		System.out.println("금호 타이어가 굴러간다.");
		
	} 
	
}
```

```java
package ch8_2;

public class Car {

	//인터페이스로 타입에 필드를 선언해준것
	//tire 의 구현 클래스를 만들고 나서 tire 의 초기값을 대입해주기
	Tire frontLeftTire = new HankookTire();  
	Tire frontRightTire = new HankookTire();
	Tire backLeftTire = new HankookTire();
	Tire backRightTire = new HankookTire();
	
	void run() {
		frontLeftTire.roll();
		frontRightTire.roll();
		backLeftTire.roll();
		backRightTire.roll();
		
	}
	
}
```

 **< 실행클래스 1 >**

```java
package ch8_2;

//실행클래스
public class CarExample {

	public static void main(String[] args) {
		Car myCar = new Car();
		myCar.run();
		
	
	}
}
```

 **< 실행클래스 2>**

```java
package ch8_2;

//실행클래스
public class CarExample {

	public static void main(String[] args) {
		Car myCar = new Car();
		myCar.run();
		
		//원래는 위에 까지만 코드가 있을때는 Car 클래스에서 한국타이어 가 필도로 대입되어서
		//한국타이어의 메소드밖에 실행이 안됫지만
		//아래처럼
		//다른 구현객체로 교체하게 되면 실행결과가 달라진다.
		myCar.frontLeftTire = new KumhoTire(); 
		myCar.frontRightTire = new KumhoTire();
		
		myCar.run();  // 각타이어의  roll 메소드를 호출하게 된다.
	}
}
```

 실행결과

	public static void main(String[] args) {
		Car myCar = new Car();
		myCar.run(); 일때는 HankookTire() 클래스가 인터페이스 필드로 적용됬기 때문에 

           HankookTire() 클래스의 메소드가 실행결과로 나타난다.

**<실행클래스 1>**

![Untitled](chap%2008-2_%20aa0ed/Untitled.png)

  

**<실행클래스 2>**

그 밑에 구현객체 대입을 바꿔주면 roll() 메소드의 

구현클래스가 달라기기때문에 실행결과도 아래와 같이 나타난다.

![Untitled](chap%2008-2_%20aa0ed/Untitled%201.png)

## 매개 변수의 다형성

**자동 타입 변환**은 필드의 값을 대입할 때에도 발생하지만,

주로 **메소드를 호출할 때 많이 발생**합니다.

이번에는 매개 변수를 인터페이스 타입으로 선언하고 호출할 때에는 구현 객체를 대입한다.

예를 들어, 다음과 같이 Driver 클래스에는 drive() 메소드가 정의되어 있다

Vehicle 타입의 매개 변수가 선언되어 있다.

```java
publc class Driver {
	public void drive(Vehicle vehicle) {
		vehicle.run();		

	}
}
```

Vehicle 을 다음과 같이 인터페이스 타입이라고 가정해보면

```java
public interface Vehicle {
	public void run();

}
```

만약  Bus 가 구현 클래스라면 다음과 같이 Driver driver() 메소드를 호출할 때

Bus 객체를 생성해서 매개값으로 줄 수 있다.

![Untitled](chap%2008-2_%20aa0ed/Untitled%202.png)

인터페이스가 매개변수로 선언이 되면 drive 라는 메소드를 호출할때는 

매개값으로 구현객체를 대입할수 있다.

그래서 어떠한 구현객체든 대입이 가능하다.

그래서 run은 매개변수에 대입된 구현객체로 실행이 된다.

구현객체 대입에 따라 실행결과 달라짐

이게 바로 매개변수의 다형성

저자리에 bus 가 오게 된것은 바로 Vehicle 타입으로 타입변환이 이뤄진것

run 은 bus에서 재정의된 run 이 실행이 되는것이고.

🟠 **여기서 잠깐**

인터페이스는 메소드의 매개 변수로 많이 등장한다.

인터페이스 타입으로 매개 변수를 선언하면 메소드 호출시 매개값으로 

여러 가지 종류의 구현 객체를 줄 수 있고 때문에 메소드 실행결과가 다양하게 나온다.

>> 매개변수의 다형성

useRemoteControl() 메소드의 매개변수가 RemoteControl 인터페이스 타입일 경우,

매개값으로 Television  객체 또는 Audio 객체를 선택적으로 줄 수 있다.

메소드 호출시 어떤 구현 객체를 매개값으로 주느냐에 따라서 

useRemoteControl() 메소드의 실행결과는 다르게 나온다.

 **소스예제 (매개변수 다형성_인터페이스)**

```java
package ch8_2.exam02;

public class Driver {  
	public void drive(Vehicle vehicle) {
		// Vehicle 인터페이스가 매개변수 타입으로 사용됨 
		//따라서 drive 라는 메소드를 호출할때 매개변수 자리 () 안에는 다향한 구현객체가 대입될수 있다.
		
		vehicle.run(); //런을 호출하게 되면 매개변수자리() 에 대입된 구현객체의 run이 호출되게 된다.
		
	}
}
```

```java
package ch8_2.exam02;

public interface Vehicle {
	public void run();
}
```

```java
package ch8_2.exam02;

//구현클래스
public class Bus implements Vehicle {
	
	@Override
	public void run() {
		System.out.println("버스가 달립니다.");
		
	}

}
```

```java
package ch8_2.exam02;

//구현클래스
public class Taxi implements Vehicle {
	
	@Override
	public void run() {
		System.out.println("택시가 달립니다.");
		
	}

}
```

```java
package ch8_2.exam02;

//실행클래스
public class DriverExample {

	public static void main(String[] args) {
		
		Driver driver = new Driver();
		
		Bus bus = new Bus();
		Taxi taxi = new Taxi();
		
		//1번
		//위에 new 해줄 필요 없이 이렇게 바로 메소드를 호출 할 수 도 있고 
		//driver.drive(new Bus());
		//driver.drive(new Taxi());
		
		//2번
		// 객체를 만든다음에 그 객체를 매개변수에 넣어서 메소드를 호출할수도 잇다
		//drive(인터페이스 매개변수) 로 선언이 되어있기때문에 어떤 구현객체로든 대입이 가능하다.
		//구현객체에 따라 실행결과 달라짐
		driver.drive(bus);
		driver.drive(taxi);
		
	}

}
```

 실행결과

![Untitled](chap%2008-2_%20aa0ed/Untitled%203.png)

## 강제 타입 변환

구현 객체가 인터페이스 타입으로 자동 타입 변환하면 

인터페이스에 선언된 메소드만 사용 가능하다는 제약 사항이 따른다.

구현클래스에 선언된 필드와 메소드를 사용해야 할 경우도 발생한다.

이때 강제 타입 변환을 해서 구현클래스 타입으로 변환한 다음, 

구현 클래스의 필드와 메소드를 사용할 수 있다.
