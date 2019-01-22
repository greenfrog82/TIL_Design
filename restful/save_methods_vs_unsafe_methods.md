# Safe methods vs Unsafe methods

HTTP method는 `Safe method`와 `Unsafe method`로 나뉠 수 있다. 

## Safe Method

만약, HTTP method가 서버의 상태를 바꾸지 않는다면 **safe method**이다. 다시 말해서, 해당 method가 read-only operation을 수행한다면 **safe**이다. 다음 나열 된 HTTP method들은 **safe**하다. 

* GET
* HEAD
* OPTIONS

모든 **safe method**들은 또한 [idempotent](./idempotent.md)하며, **cache**될 수 있다.  

비록 safe method들이 read-only의 의미를 가지고 있더라도, 서버는 safe method에 의한 접근을 로깅하거나 통계 자료를 생성하는 등 상태를 변경할 수 있다. 하지만 safe method가 중요한 이유는 클라이언트가 이러한 메소드를 통해 서버를 변경하지 않는다는 것이다. 결국 서버에 불필요한 로드나 부담을 주지 않게된다. 브라우저는 서버에 어떤 해로운 영향에 대한 걱정 없이 safe method를 호출할 수 있다. 웹 크롤러 역시 safe method를 호출하는 것에 의존한다.  

safe method는 오직 static file들만 서빙할 필요는 없다. 서버는 safe method에 대해서 동적인 응답을 줄 수 있으며, 이러한 동적인 응답은 외부에 영향을 끼치지 않아야한다. 예를들어, e-commerce 서비스에서 GET method에 대한 동작이 주문을 발생시켜서는 안된다. 

safe method를 옳바르게 구현하는 것은 Apache, nginx 또는 ISS와 같은 서버 어플리케이션의 책임이다. 특히, 서버 어플리케이션은 GET method가 서버의 상태를 변경하지 않도록 해야한다.  

## UnSafe Method

HTTP method가 서버이 상태를 바꾼다면 **unsafe method**이다. 다시 말해서, 해당 mehtod가 write, delete, update operation을 수행한다면 **unsafe method**이다. 다음 나열 된 HTTP methode들은 **unsafe**하다.

* POST
* PUT
* PATCH
* DELETE

**unsafe method**의 경우 `PUT`과 `DELETE` method만이 [idempotent](./idempotent.md)이다.  

# Reference

* [Safe](https://developer.mozilla.org/en-US/docs/Glossary/safe)
* [What are idempotent and/or safe methods?](http://restcookbook.com/HTTP%20Methods/idempotency/)
* [Method Definitions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)