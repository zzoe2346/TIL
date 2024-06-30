# MethodArgumentNotValidException 처리
## 무슨 문제?
스프링과 타임리프로 SSR를 이용한 상품 관리용 관리자 페이지를 만드는데 클라이언트에서 잘못된 POST HTTP를 날리면 `MethodArgumentNotValidException` 이 발생함. 그런데 이걸 catch하려고 Controller Class의 이를 처리하는 Method에 아무리 try-catch를해도 예외가 안잡혔다. 

## 원인
`MethodArgumentNotValidException` 는 Spring MVC에서 Controller에 전달되기전 VIEW,MODEL 에서 예외가 발생해서 컨트롤러 안에서는 catch가 불가했던것임. 
## 해결 방법

`@ControllerAdvice`는 전역 예외 처리가 가능 + 컨트롤러 예외처리 가능!
`@ExceptionHandler(MethodArgumentNotValidException.class)`로 `MethodArgumentNotValidException`을 catch해서 `"version-SSR/product-error"` 페이지로 리턴해줌
## 배움
- `@ControllerAdvice` 로 전역 예외 처리가 가능한 사실을 처음 알게됨. 
- Spring MVC에 관해 더 알아야겠다는 생각! Controller 외부에서 예외가 발생할것이라는 생각은 전혀 하지 못했다.
## ⭐️더 자세히 by ChatGPT
`MethodArgumentNotValidException`는 Spring MVC에서 요청이 컨트롤러 메서드에 도달하기 전에 데이터 바인딩 및 유효성 검사 과정에서 발생합니다. 이 예외는 주로 다음 위치에서 발생합니다:

1. **요청 데이터 바인딩 단계**: Spring MVC는 요청 데이터를 컨트롤러 메서드의 파라미터로 바인딩합니다. 이 과정에서 `@Valid` 어노테이션이 적용된 객체에 대해 유효성 검사를 수행합니다. 만약 유효성 검사에 실패하면 `MethodArgumentNotValidException` 예외가 발생합니다.

2. **HandlerMethodArgumentResolver**: Spring MVC는 `HandlerMethodArgumentResolver`를 사용하여 컨트롤러 메서드의 파라미터를 해결합니다. 이 과정에서 유효성 검사 어노테이션이 있는 경우, `MethodArgumentNotValidException`이 발생할 수 있습니다.

예를 들어, 컨트롤러 메서드가 다음과 같을 때:

```java
@PostMapping("/products")
public ResponseEntity<Product> createProduct(@Valid @RequestBody Product product) {
    // Product 객체가 유효한 경우 비즈니스 로직 수행
    return ResponseEntity.ok(product);
}
```

여기서 `@Valid` 어노테이션이 `Product` 객체에 적용되어 있습니다. `Product` 객체의 필드에 대해 유효성 검사가 실패하면, Spring은 컨트롤러 메서드에 도달하기 전에 `MethodArgumentNotValidException`을 발생시킵니다.

### Spring MVC 처리 흐름

1. **클라이언트 요청**: 클라이언트가 `/products` 엔드포인트에 POST 요청을 보냅니다.
2. **디스패처 서블릿**: 요청을 받아 적절한 핸들러(컨트롤러 메서드)를 찾습니다.
3. **HandlerMapping**: 요청 URL과 컨트롤러 메서드를 매핑합니다.
4. **HandlerAdapter**: 컨트롤러 메서드를 호출하기 위해 필요한 파라미터를 준비합니다. 이 단계에서 `@Valid` 어노테이션이 적용된 파라미터에 대해 유효성 검사를 수행합니다.
5. **유효성 검사**: `Product` 객체의 유효성 검사가 수행되고, 유효하지 않은 경우 `MethodArgumentNotValidException`이 발생합니다.
6. **예외 처리**: 예외가 발생하면 `@ControllerAdvice`로 설정된 전역 예외 처리기가 이 예외를 처리합니다.

### 전역 예외 처리기

전역 예외 처리기를 설정하여 `MethodArgumentNotValidException`을 처리하는 방법은 다음과 같습니다:

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    public String handleValidationExceptions(MethodArgumentNotValidException ex) {
        return "version-SSR/product-error";
    }
}
```

이 예외 처리기는 `MethodArgumentNotValidException`이 발생했을 때 호출되며, HTTP 응답 상태 코드를 `400 Bad Request`로 설정하고 "version-SSR/product-error" 뷰를 반환합니다.

### 예제 코드

컨트롤러와 예외 처리기를 포함한 예제 코드를 다시 확인해 보겠습니다.

#### 컨트롤러 클래스

```java
@RestController
public class ProductController {

    @PostMapping("/products")
    public ResponseEntity<Product> createProduct(@Valid @RequestBody Product product) {
        // Product 객체가 유효한 경우 비즈니스 로직 수행
        return ResponseEntity.ok(product);
    }
}
```

#### 전역 예외 처리기

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    public String handleValidationExceptions(MethodArgumentNotValidException ex) {
        return "version-SSR/product-error";
    }
}
```

#### Product 클래스 (유효성 검사가 필요한 DTO)

```java
public class Product {

    @NotNull(message = "Product name cannot be null")
    private String name;

    @Min(value = 1, message = "Price should be greater than zero")
    private BigDecimal price;

    // Getters and setters
}
```

위 코드에서 `ProductController`는 `Product` 객체를 요청 본문에서 받아 처리합니다. `@Valid` 어노테이션이 적용된 `Product` 객체는 유효성 검사를 거치게 됩니다. 만약 `Product` 객체가 유효하지 않다면, `MethodArgumentNotValidException`이 발생하며, 이 예외는 전역 예외 처리기에서 처리됩니다.

