---
layout: post
title: "Fibonacci Sequence in Swift 5"
date: 2020-06-09 01:00:00 +0700
published: true
author: Zhengyu Ren
---

{% highlight swift %}
struct Fibonacci: Sequence {
    let by: Int
    
    func makeIterator() -> FibonacciIterator {
        return FibonacciIterator(self)
    }
}

struct FibonacciIterator: IteratorProtocol {
    let fibonacci: Fibonacci
    var firstTime: Bool = true
    var secondTime: Bool = false
    var thirdLast, secondLast, last: Int?
    
    init(_ fibonacci: Fibonacci) {
        self.fibonacci = fibonacci
    }

    mutating func next() -> Int? {
        if firstTime {
            firstTime = false
            secondTime = true
            last = 0
            return last
        }
        if secondTime {
            secondTime = false
            secondLast = last
            last = 1
            return last
        }
        thirdLast = secondLast
        secondLast = last
        last = thirdLast! + secondLast!
        if last! > fibonacci.by {
            return nil
        }
        return last
    }
}


let fibo = Fibonacci(by: 100000000)
for n in fibo {
    print(n)
}
{% endhighlight %}
