# SpringBoot 기동 시 FileNotFoundException 발생

### SpringBoot 기동 시, 서버 기동 및 기능 수행에는 문제가 없으나 특정 jar파일을 대상으로 FileNotFoundException 발생함
- Tomcat 사용 시 Context.xml 파일 수정으로 해결 가능
- application.yml 에서 설정하는 방법으로도 해결 가능
- 포트 설정과 관련된 이유로, config.java 파일에서 설정하는 방법으로 해결함

```java

@Configuration
public class config {

    @Bean
    public EmbeddedServletContainerFactory getEmbeddedServletContainerFactory() {
    	TomcatEmbeddedServletContainerFactory containerFactory = new TomcatEmbeddedServletContainerFactory() {
		@Override
		protected void postProcessContext(Context context) {
			Set<String> pattern = new LinkedHashSet<String>();
			pattern.add("filename.jar");
			StandardJarScanFilter filter = new StandardJarScanFilter();
			filter.setTldSkip(StringUtils.collectionToCommaDelimitedString(pattern));
			((StandardJarScanner)context.getJarScanner()).setJarScanFilter(filter);
		}
	};
		
	return containerFactory;
    }
}
```   
