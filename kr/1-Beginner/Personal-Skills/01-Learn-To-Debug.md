# Learn to Debug
[//]: # (Version:1.0.0)
Debugging is the cornerstone of being a programmer. The first meaning of the verb "debug" is to remove errors, but the meaning that really matters is to see into the execution of a program by examining it. A programmer that cannot debug effectively is blind.

* 디버깅은 프로그래머로서의 주춧돌이다. '디버그'의 사전적 정의는 에러를 고치는 것이나, 그 의미는 프로그램을 실행함으로서 진짜 문제를 검사하는 것이다. 프로그래머는 보지않고 효율적으로 디버그할 수 없다. 


Idealists, those who think design, analysis, complexity theory, and the like are more fundamental than debugging, are not working programmers. The working programmer does not live in an ideal world. Even if you are perfect, you are surrounded by and must interact with code written by major software companies, organizations like GNU, and your colleagues. Most of this code is imperfect and imperfectly documented. Without the ability to gain visibility into the execution of this code, the slightest bump will throw you permanently. Often this visibility can be gained only by experimentation: that is, debugging.

* 디자인, 분석, 복잡한 이론이 디버깅보다 더 기본적이라고 생각하는 이상주의자들은 개발자와 일하고있지 않을 것이다. 개발자들은 이상적인 세상에 살지않는다. 비록 당신이 완벽하더라도 당신은 소프트웨어 회사, GNU와 같은 조직, 당신의 동료들이 작성한 코드에 둘러쌓여 있고, interact 해야한다. 대부분의 이 코드는 완벽하지 않고 완벽히 문서화도 되지않았다. 코드의 실행에 대한 통찰력이 없다면, 최소한의 bump(균열?, 뭐 등)가 널 영구히 throw해버릴 것이다. 대개 이 통찰력은 경험을 통해서만 얻어진다. : 그것이 디버깅이다.  

Debugging is about the running of programs, not programs themselves. If you buy something from a major software company, you usually don't get to see the program. But there will still arise places where the code does not conform to the documentation (crashing your entire machine is a common and spectacular example), or where the documentation is mute. More commonly, you create an error, examine the code you wrote, and have no clue how the error can be occurring. Inevitably, this means some assumption you are making is not quite correct or some condition arises that you did not anticipate. Sometimes, the magic trick of staring into the source code works. When it doesn't, you must debug.

* 디버깅은 프로그램에 실행에 관한 것이지, 프로그램 자체에 관한 것은 아니다. 당신이 소프트웨어 회사로부터 어떤 것을 구매하면, 프로그램을 보기위해 얻는 것은 아닐 것이다. 그러나 문서를 따르지않고, 문서가 없다면 여전히 발생할 것이다. 대부분, 오류를 만들고, 작성한 코드를 검사해봐도 어떻게 에러가 발생했는 지 단서가 없다. 필연적으로, 이것은 당신이 틀렸거나, 몇몇 조건을 예상하지 못한 것을 의미한다. 때때로, magic trick of 째려보기가 코드를 동작하게 하기도 한다. 그것이 동작하지 않을 때, 필수로 디버그 해야한다. 

To get visibility into the execution of a program you must be able to execute the code and observe something about it. Sometimes this is visible, like what is being displayed on a screen, or the delay between two events. In many other cases, it involves things that are not meant to be visible, like the state of some variables inside the code, which lines of code are actually being executed, or whether certain assertions hold across a complicated data structure. These hidden things must be revealed.

* 프로그램의 실행에 관한 통찰력을 갖기 위해서는 코드를 실행해보고 그것을 관찰해야 한다. 화면에 출력됨과, 두 이벤트 사이에 딜레이를 통해 가끔 보이기도 한다. 많은 경우에, 코드 내부 변수의 조건과 같은 의도하지 않았던 것이 끌여들여지는 것이 보인다면, 어느 줄이 실행될 떄 일어났는지, 복잡한 자료구조 간에 생겼는지. 그 숨은 것을 반드시 들춰야 한다.

The common ways of looking into the ‘innards’ of an executing program can be categorized as:

* 프로그램 실행의 내부를 보는 보편적 방법을 나누면:

- Using a debugging tool,
- Printlining - Making a temporary modification to the program, typically adding lines that print information out, and
- Logging - Creating a permanent window into the programs execution in the form of a log.

* - 디버깅 툴을 사용한다.
* - 라인별 출력 해보기 - 프로그램을 잠시 수정해, 필요한 정보가 출력되도록 한다.
* - 로그 남기기 - 프로그램의 실행되는 내부를 볼 수 있는 영구적인 창인 로그를 남기도록 한다. 

Debugging tools are wonderful when they are stable and available, but printlining and logging are even more important. Debugging tools often lag behind language development, so at any point in time they may not be available. In addition, because the debugging tool may subtly change the way the program executes it may not always be practical. Finally, there are some kinds of debugging, such as checking an assertion against a large data structure, that require writing code and changing the execution of the program. It is good to know how to use debugging tools when they are stable, but it is critical to be able to employ the other two methods.

* 디버깅 도구는 굉장히 안정적이고 도움이 되나, printlining 과 로그가 더 중요하긴 하다. 디버깅 도구는 언어 개발보다 대체로 늦게 개발되는 편이기 때문에 특정 순간에 사용하지 못할 수 있다. 추가적으로, 디버깅 도구가 프로그램의 실행을 미묘하게 바꿀 수 있기 때문에 항상 실용적이지는 못 할 수 있다. 마지막으로, 몇 경우의 디버깅에서, 거대한 데이터 구조에 대한 검사를 할 때, 코드를 작성하거나 프로그램 실행에 관해 바꿔야 한다. 이것은 여러분이 디버깅 도구를 어떻게 하면 안정적으로 사용할 수 있을지 알려주는 것이나 이것은 다른 두 방법에 비해 사용하는 데 치명적일 수 있다.

Some beginners fear debugging when it requires modifying code. This is understandable - it is a little like exploratory surgery. But you have to learn to poke at the code and make it jump; you have to learn to experiment on it and understand that nothing that you temporarily do to it will make it worse. If you feel this fear, seek out a mentor - we lose a lot of good programmers at the delicate onset of their learning to this fear.

* 몇몇 주니어 개발자 들은 코드를 코드를 수정해야만 하는 디버깅을 할 때 공포를 느낀다. 이해는 간다. 그것은 작은 실험 수술 같은 것이다. 그러나 당신은 코드를 건드는 법을 배워야 하고 그것이 뛰게 만들어야 한다. 당신은 경험을 통해 배워야 하고 일시적으로 그것을 더 안좋게 만들 수 있다는 것을 이해해야 한다. 만약 당신이 이 공포를 느낀다면, 멘토를 찾아라. 우리는 이 두려움에 떨게하는 작은 학습의 시작에서 좋은 프로그래머들을 잃는다.


Next [How to Debug by Splitting the Problem Space](02-How-to-Debug-by-Splitting-the-Problem-Space.md)
