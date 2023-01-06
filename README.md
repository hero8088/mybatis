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
			)
		}
	</update>


# 모든 row가 Null일 때 컬럼이 생략되는 경우 Mapper-Config.xml파일에 
	<setting name="callSettersOnNulls" value="true"/>
  추가 [result type이 HashMap인경우 생략되는거 같다]

# IN 안에 파라메터 줄 때는 IN ('${PARA}')
