## __Spring 기초__
---
@Controller : 컨트롤러 클래스 어노테이션
<br>
@RequestMapping() : URL 매핑 기능
<br><br>

### __Controller 화면 처리__
1. void 메서드의 페이지 이동 : 일반적인 경우 맵핑 URL의 경로를 파일의 이름으로 사용한다.
```java
@RequestMapping(value="/req_ex01")
public void req_ex01(){
}
```
<br>

2. String 메서드의 페이지 이동 : view 폴더 아래의 jsp파일로 이동한다.
```java
@RequestMapping(value="/req_ex01")
public String req_ex01(){
    return "req_ex01()";
}
```
<br>

3. redirect 페이지 이동 : 리다이렉트 키워드를 이용해 다시 브라우저로 요청한다.
```java
@RequestMapping(value="/req_ex01")
public String req_ex01(){
    return "redirect:/req_ex01";
}
```
<br>

### __메서드에서 요청 파라미터 값의 처리 방법__
1. HTTPServletRequest 객체를 이용한 HTTP 전송 정보를 얻는다.
   - HTTPServletRequest 객체를 활용한다.
   - HandlerMapping이 메서드를 찾아서 해당 메서드 전체를 가져온다.
```java
@PostMapping("/join")
public String register(HttpServletRequest request) {
	System.out.println("/request/join: POST");
		
	System.out.println("ID: " + request.getParameter("userid"));
	System.out.println("PW: " + request.getParameter("userpw"));
	System.out.println("Hobby: " + Arrays.toString(request.getParameterValues("hobby")));
		
	return "request/join";
}
```
<br>

2. @RequestParam 어노테이션을 이용한 HTTP 전송 정보를 얻는다.
   - @RequestParam은 반드시 값이 존재해야 한다.
   - required = false로 설정할 시, 값이 반드시 존재하지 않아도 된다.
   - defaultValue를 이용해 사용자가 default값을 설정할 수 있다.

```java
@PostMapping("/join")
public void register(@RequestParam("userid") String id,
					@RequestParam("userpw") String pw,
					@RequestParam(value="hobby", 
                    required = false, defaultValue = "no hobby person") List<String> hobbys) {
		
	System.out.println("ID: " + id);
	System.out.println("PW: " + pw);
	System.out.println("HOBBY: " + hobbys);
}
```
<br>

3. 커맨드 객체를 이용한 HTTP 전송 정보를 얻는다.
   - handleradapter가 UserVO 객체를 찾아서 보내준다.
   - VO객체 전체를 불러와서 정보를 보여주는 방식이다.
   - VO객체에 동일한 setter가 있다면 자동으로 저장되는 방식이다.

```java
@PostMapping("/join")
public void register(UserVO user) {
		
	System.out.println(user);
}
```
<br>

### __Model 전달자 : 화면에 데이터를 전달하기 위한 객체__
1. Model 객체
   - Model 타입을 메서드의 파라미터로 주입하게 되면 view로 전달하는 데이터를 담아서 보낼 수 있다.
   - request.setAttribute()와 유사한 역할을 한다.

```java
@GetMapping("/test")
public void test(@RequestParam("age") int age, Model model) {
		
	//파라미터로 받은 값을 model에 담는다.
	model.addAttribute("age", age);
	//사용자가 지정한 값을 model에 담는다.
	model.addAttribute("nick", "멍멍이");
	//이후 handleradapter가 model객체 자체를 가져간다. -> 이를 test.jsp에 뿌린다.
}
```
<br>

2. @ModelAttribute 어노테이션
   - 전달 받은 파라미터를 Model에 담아서 화면까지 전달하려 할 때 사용된다.

```java
@GetMapping("/test")
public void test(@ModelAttribute("age") int age, Model model) {
	model.addAttribute("nick", "멍멍이");
}
```
<br>

3. ModelAndView 객체

```java
@GetMapping("/test2")
public ModelAndView test2() {
		
	//ModelAndView객체를 따로 생성해서 값을 넣고 그 자체를 보내는 방식이다.
	ModelAndView mv = new ModelAndView();
	mv.addObject("userName", "김철수");
	//정보를 담아 화면으로 보여지고 싶은 파일도 지정할 수 있다.
	mv.setViewName("/response/test2");
		
	//데이터를 하나만 보낼 경우 아무것도 안쓰고 return new ModelAndView("/response/test2","userName","홍길동");이런 식으로 입력할 수 있다.
	return mv;
}
```
<br>

4. RedirectAttribute 객체

```java
@PostMapping("/login")
public String login(@RequestParam("userid") String id, @RequestParam("userpw") String pw,
					@RequestParam("userpwchk") String pwchk,
					RedirectAttributes ra) {
	System.out.println("/login: POST 요청 발생!");
	System.out.println("ID: " + id);
	System.out.println("PW: " + pw);
	System.out.println("CHK:" + pwchk);
		
	if(id.equals("")) {
		//model.addAttribute("msg", "아이디는 필수값이에요!"); -> 이런식으로 model에 넣어 직접 보내버리면 요청에 대한 응답에서는 보여지지만
		//다시 재요청할 땐 소멸해버린다. 따라서 파라미터값으로만 들어오고 화면에 보여지는건 없음
		//해결방안 : RedirectAttributes를 이용한다.
		ra.addFlashAttribute("msg", "아이디는 필수값이에요!");
		//addFlashAttribute는 한번 보여주고 끝남 새로고침하면 없어짐.
			
		//redirect로 다시 처음의 로그인 화면이 보일 수 있도록 한다.
		return "redirect:/response/login";
	}else if(!pw.equals(pwchk)) {
		ra.addFlashAttribute("msg", "비밀번호 확인란을 체크하세요!");
		return "redirect:/response/login";
	}
		
	return "";	
}
```