# 서버 가동 자체가 안되던 문제 수정
>**원인** : WriteDAO.xml 의 view.do resultType의 경로가 잘못되어 수정함.

기존
```xml
<!-- view.do -->
	<select id="selectByUid" resultType="com.lec.spring.WriteDTO">
```

수정 후
```xml
<!-- view.do -->
	<select id="selectByUid" resultType="com.lec.spring.domain.WriteDTO">
```
##

# 글 수정 시 수정은 가능하나 수정하기를 누를 시 에러가 나는 것 수정

>**원인** : 글 수정 시 updateOk.jsp에 ${uid}여서 uid값이 안 넘어옴. ${param.uid}로 수정함.

기존
```html
	<c:otherwise>
		<script>
			alert("수정 성공");
			location.href = "view.do?uid=${uid}";
		</script>
	</c:otherwise>
  ```
  
  수정 후
  
  ```html
	<c:otherwise>
		<script>
			alert("수정 성공");
			location.href = "view.do?uid=${param.uid}";
		</script>
	</c:otherwise>
  ```

##
# 글 삭제시 에러가 나는 것 수정

>**원인** : 글 삭제 시 WriteDAO.xml의 삭제 쿼리가 WHERE uid로만 되어 있어 wr_uid로 수정함.

기존
```xml
	<!--  글 삭제 -->
	<delete id="deleteByUid" flushCache="true">
		DELETE FROM test_write WHERE uid = #{uid}
	</delete>
  ```
  수정 후
  
  ```xml
	<!--  글 삭제 -->
	<delete id="deleteByUid" flushCache="true">
		DELETE FROM test_write WHERE wr_uid = #{uid}
	</delete>
  ```
