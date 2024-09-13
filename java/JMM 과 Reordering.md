## Background
  - Leetcode에서 [문제](https://leetcode.com/problems/print-in-order/) 를 풀다가 `JMM(Java Memory Model)`과 `re-ordering` 이해하기 위해 작성
  - 처음 아래 솔루션을 작성했으나, 원하는 결과가 나오지 않음.
    - static 변수로 멀티 스레드에서 접근할 수 있는 공유자원을 만들어두고, 해당 공유자원을 통해 순서를 보장하도록 작성한 것이 의도.
    ``` java
    class Foo {
        private static boolean isFirstCalled = false;
        private static boolean isSecondCalled = false;
    
        public Foo() {
            
        }
    
        public void first(Runnable printFirst) throws InterruptedException {
    
            // printFirst.run() outputs "first". Do not change or remove this line.
            printFirst.run();
            isFirstCalled = true;
        }
    
        public void second(Runnable printSecond) throws InterruptedException {
            while (!isFirstCalled) {}
            // printSecond.run() outputs "second". Do not change or remove this line.
            printSecond.run();
            isSecondCalled = true;
        }
    
        public void third(Runnable printThird) throws InterruptedException {
            while (!isFirstCalled || !isSecondCalled) {}
            // printThird.run() outputs "third". Do not change or remove this line.
            printThird.run();
        }
    }
    ```
  - GPT 한테 물어보니, JMM에서는 reoreding이 발생해 코드의 작성 순서와 다른 수행이 가능하다고 한다.
  - Reordering이 뭔데..?
## Study
- 내가 원하는 방식대로 동작하지 않는 원인은 `Reordering` 때문이라고 한다.
- 
## Conclusion
- 
## Keywords
`Reordering`, `JMM`, `Sequential consistency`, `JSR-133`, `atomic`, `happens-before`, `data race`, `synchronized`
## Reference
- [1] https://amanda-ariyaratne.medium.com/how-program-reordering-breaks-double-checked-locking-in-java-2756db827523
- [2] https://jenkov.com/tutorials/java-concurrency/java-happens-before-guarantee.html
- [3] https://docs.oracle.com/javase/specs/jls/se22/html/jls-17.html#jls-17.4
