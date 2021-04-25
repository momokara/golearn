# 第02周作业提交

个人觉得应该dao层应该 Wrap 这个 error
因为事务的边界不在 dao  层上，而是在 Service 层上，假如一个业务逻辑调用了两个 dao  的方法（A、B）组成一个事务体，若 A 正常执行了，
而 B 执行时却发生了异常，这时 A 的执行就需要回滚，若将 B 中的异常捕获了，那根本就不知道 B 是正常执行而是异常执行了，
也无法处理事务了

```
// 使用 github.com/pkg/errors 抛出错误

// example
err := errors.New("whoops")
// or
err := errors.Errorf("whoops: %s", "foo")

// 我们需要附加信息时
cause := errors.New("whoops")
err := errors.Wrap(cause, "oh noes")

// 获取调用堆栈时
err := errors.New("whoops")
fmt.Printf("%+v", err)


```
