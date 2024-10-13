# 캐시문제 : 한트랜잭션안에 동일쿼리를 실행 시킬 때 
             2번째 부터는 캐시에 저장된 메모리주소값을 던지는 문제
             때문에 서비스에서 서로 다른 변수로 받더라도 같은 결과 주소를 가진다.
  해결 : select xml에 다음 값을 셋팅한다. flushCache="true" useCache="false"
  주의 : 메모리문제를 야기 할 수 있으므로 꼭 필요한 경우에만 사용
  
  
프로시저 실행
https://stylishc.tistory.com/103


	<!--Procedure Call -->
	<update id="copy" statementType="CALLABLE" parameterType="HashMap">
		{ CALL PRC_TPMS_ACTY_COPY_PROJ(
				#{pjtNo}
				#{OUT_RESULT, mode=OUT, jdbcType=VARCHAR} <!-- 프로시져에서 돌려받을 값 설정 -->
			)
		}
	</update>


# 모든 row가 Null일 때 컬럼이 생략되는 경우 Mapper-Config.xml파일에 
	<setting name="callSettersOnNulls" value="true"/>
  추가 [result type이 HashMap인경우 생략되는거 같다]

# IN 안에 파라메터 줄 때는 IN ('${PARA}')

# IN_MAX_REV != null and IN_MAX_REV.equals("Y") 문자매칭이 안되는 경우 변수명에 _YN, _Y, 등이 포함되어 있지 않는지 확인한다.

# 대용량 데이터 조회 속도문제 : fetchSize옵션을 줘서 향상시킬수 있다.
select id="selectLabelList"  parameterType="java.util.HashMap" resultType="nHashMap" fetchSize="2000"

                              안주면 기본값이 10이어서 10000건의 경우 1000번 입출력이 발생하는데
			      fetchSize를 2000로 주면 5번만 왔다갔다 한다. 그래서 빨라짐
	                      메모리에 2000개씩 가지고 있는다는 뜻으로 남발할 경우 서버에 메모리 부족현상 발생

CLOB 컬럼 저장 시 MERGE문 쓰면 안된다... 제길슨

# selectKey 사용법 : https://yookeun.github.io/java/2014/07/11/mybatis-selectkey/
<pre>
	에디터모드에서 확인할것!!
<!--
<insert id="insertBoard" parameterType="Board">
    <selectKey resultType="string" keyProperty="boardID" order="BEFORE">
        SELECT MAX(boardID)+1 FROM board        
    </selectKey>    
    INSERT INTO board(boardID, title, content)
    VALUES(#{boardID}, #{title}, #{content})
</insert>  
-->
</pre>
