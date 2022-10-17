# 2개 이상의 포트로 접근 가능하도록 설정(SpringBoot)

### SpringBoot에서, 2개 이상의 포트로 접근 가능하도록 설정
- 당시 함께 처리한 다른 이슈(<a href="https://github.com/crp9428/Bookmark/blob/main/FileNotFoundException-jar.md" >링크</a>) 있음
- config.java 파일에서 다음과 같이 설정함 (포트 번호 등은 임의의 값으로 수정함)

```java

@Configuration
public class config {

    @Bean
    public EmbeddedServletContainerFactory getEmbeddedServletContainerFactory() {
		TomcatEmbeddedServletContainerFactory containerFactory = new TomcatEmbeddedServletContainerFactory() {
			@Override
			protected void postProcessContext(Context context) {
				// 생략
			}
		};

		containerFactory.setPort(8081);
			
        Connector connector = new Connector(containerFactory.DEFAULT_PROTOCOL);
        connector.setPort(8082);
        containerFactory.addAdditionalTomcatConnectors(connector);
		
		containerFactory.setContextPath("/contextPath");
		
		return containerFactory;
    }
}

```   