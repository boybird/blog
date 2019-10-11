---
title: "三个线程轮流打印1到100"
date: "2019-10-06"
---

### rust 解法
现在我用　rust 的channel 完成这道题,不用再100秒才能看出结果了

```rust
use std::sync::mpsc;
use std::thread;

fn main() {
    let (s1, r1) = mpsc::channel::<usize>(); // s1 告诉下个线程打印 3N+1 ， r1 接收 3N+1 的打印数字
    let (s2, r2) = mpsc::channel::<usize>(); // s2 告诉下个线程打印 3N+2 ， r2 接收 3N+2 的打印数字
    let (s3, r3) = mpsc::channel::<usize>(); // s3 告诉下个线程打印 3N+3 ， r3 接收 3N+3 的打印数字

    const MAX_PINRT: usize = 100;

    thread::spawn(move || {
        let id = thread::current().id();
        loop {
            if let Ok(message) = r2.recv() {
                println!("thread {:?} print: {}", id, message);
                if message < MAX_PINRT {
                    s3.send(message + 1).unwrap();
                } else {
                    break;              //       打印完成退出
                }
            } else {
                break;                  //       输出完成退出 
            }
        }
    });

    thread::spawn(move || {
        let id = thread::current().id();
        for val in r3 {
            println!("thread {:?} print: {}", id, val);
            if val < MAX_PINRT {
                s1.send(val + 1).unwrap();
            } else {
                break;
            }
        }
    });
    let id = thread::current().id();
    s2.send(1).unwrap();
    for val in r1 {
        println!("thread {:?} print: {}", id, val);
        if val < MAX_PINRT {
            s2.send(val + 1).unwrap();
        } else {
            break;
        }
    }
}
```