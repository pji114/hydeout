---
layout: post
title: "Spring Securiy를 이용하여 Login 기능을 구현해본다"
categories:
  - Spring-Boot
---

# 일단 WebSecurityConfigurerAdapter 클래스르 상속 받는 보안설정을 구현해보자

```java
@Configuration
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
                http.authorizeRequests()
                        .antMatchers("/user/login", "/user/logout", "/static/**", "/denied/**", "/css/**", "/js/**", "/img/**", "/scss/**", "/vendor/**")
                        .permitAll()
                        .anyRequest()
                        .authenticated()
                        ;
    }

}
```
## @Configuration
클래스를 환경설정 클래스로 선언한다
## @EnableGlobalMethodSecurity
어노테이션 기반의 보안 활성화

##configure(HttpSecurity http) 
페이지 접근권한 설정, 접근권한은 사용자의 권한으로도, 아니면 페이지 자체로도 적용할수 있다. 지금은 권한 기반이 아닌 주소기반으로 접근권한 설정을 한다.
1. http.authorizeRequests() : Security 처리에 HttpServletRequest을 사용한다는 것을 의미한다
2. .antMatchers(".....") : 해당 경로에에 위치하는 페이지들을 의미한다, 예를들어/user/login 이라하면 user경로 아래 login 파일을 의미하며 /css/** 이라하면 css 아래 모든 파일을 의미한다.
3. .permitAll() : 지금까지 설정한 모든 경로에 대해 접근권한을 허가한다.
4. .anyRequest() : 이 페이지로 들어오는 모든 요청을 의미한다.
5. .authenticated() : 이 설정이 적용된 페이지는 보안 인가가 필요하다.

##여기서 http.authorizeRequests()까지 설정의 의미
antMatchers의 [/user/login", "/user/logout", "/static/**", "/denied/**", "/css/**", "/js/**", "/img/**", "/scss/**", "/vendor/**] 경로로 들어오는 요청은 permitAll 설정에 따라 모두 허가한다
그리고 anyRequest 이 설정에 따라 나머지 모든 요청은 authenticated 이 설정에 의해 인증이 필요하다

# Spring Security가 제공해주는 기본적인 로그인 페이지 접근설정

```java
 http.formLogin()
          .defaultSuccessUrl("/main")
          .successHandler(authenticationSuccessHandler)
          .failureHandler(authenticationFailureHandler);

```

## formLogin()
말 그대로 로그인 폼을 어떻게 할래? 라는 설정이다.
### 기본 로그인 페이지 설정 (로그인 컨트롤러 필요없다.)
1. defaultSuccessUrl : 로그인이 성공했을때 기본적으로 리다이렉트 될 페이지 주소다
2. successHandler : 로그인 성공시 처리해야 될 작업이 있다면 성공 핸들러를 만들어 두고 여기 등록 해 둔다
3. failureHandler : 로그인 실패시 처리해야 될 작업이 있다면 실패 한들러를 만들어 두고 여기 등록 해 둔다.

위 처럼 설정하면 Spring Security가 제공 해주는 기본적인 로그인 페이지를 볼수 있다
<img src="/_screenshots/Security_Default_Login.png" width="450px" height="300px" title="기본 로그인 화면"></img>

### 커스텀 로그인 페이지 설정(로그인 컨트롤러 필요함)
여백의 미를 사랑하고 디자인 따위는 사치라고 생각하는 사람이면 위처럼 써도 무방하나(~~귀찮거나~~) 보통은 사이트 용도에 맞도록 수정해서 로그인 페이지를 쓸것이다. 그럴떈 아래처럼 쓰자

```java
http.formLogin()
                .loginPage("/user/login")
                .usernameParameter("userId")
                .passwordParameter("password")
                .defaultSuccessUrl("/main")
                .successHandler(authenticationSuccessHandler)
                .failureHandler(authenticationFailureHandler);

```

1. loginPage : 로그인 페이지의 주소 설정
2. usernameParameter : 로그인 페이지에서 userName(ID로 쓸 파라미터)을 어떤 이름으로 받아올건지 정의한다.
3. passwordParameter : 로그인 페이지에서 password(비밀번호로 쓸 파라미터)을 어떤 이름으로 받아올건지 정의한다.
4. defaultSuccessUrl : 로그인이 성공했을때 기본적으로 리다이렉트 될 페이지 주소다
5. successHandler : 로그인 성공시 처리해야 될 작업이 있다면 성공 핸들러를 만들어 두고 여기 등록 해 둔다
6. failureHandler : 로그인 실패시 처리해야 될 작업이 있다면 실패 한들러를 만들어 두고 여기 등록 해 둔다.

위처럼 설정하면 아래와 같이 커스텀한 로그인 페이지를 볼수있다.
<img src="/_screenshots/Custom_Login.png" width="450px" height="300px" title="커스텀 로그인 화면"></img>