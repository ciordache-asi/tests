# tests
tests repo

```java
@Path("")
public class ZAJobLauncher {
	@Autowired
    JobLauncher jobLauncher;

    @Autowired
    Job expcmdJob;
    
	@Path("launchZAJob")
	public void launchZAJob(List<String> idenetetesupport) throws Exception {
		String listIdenetetesupport="";
		idenetetesupport.forEach((identetesupport) -> listIdenetetesupport+=identetesupport+",");
		JobParameters params = new JobParameters();
		params.getParameters().put("listIdentetesupport", new JobParameter(listIdenetetesupport));
//		params.getParameters().put("filePath", new JobParameter("c:/wrk/tmp/testFixedLength.txt"));
		
		 jobLauncher.run(expcmdJob, params);
		 
		 
		 jobLauncher.run(expcmdJob, 
				 (new JobParametersBuilder()).addString("listIdenetetesupport",listIdenetetesupport).toJobParameters() );
	}
  }
```

---------------------------------------

Exemple @Query mapping to DTO : https://stackoverflow.com/a/36109273

```java
@Repository
public class StatementNativeRepository {      
    @PersistenceContext private EntityManager em;

    static final String STATEMENT_SQLMAP = "Statement-SQL-Mapping";

    public List<StatementDto> findPipelinedStatements() {
        Query query = em.createNativeQuery(
            "select author_name, create_time from TABLE(SomePipelinedFun('xxx'))",
            STATEMENT_SQLMAP);
        return query.getResultList();
    }

    @SqlResultSetMapping(name= STATEMENT_SQLMAP, classes = {
        @ConstructorResult(targetClass = StatementDto.class,
            columns = {
                @ColumnResult(name="author_name",type = String.class),
                @ColumnResult(name="create_time",type = Date.class)
            }
        )
    }) @Entity class SQLMappingCfgEntity{@Id int id;} // <- walkaround
}
```

--------
Un autre exemple de mapping de dto : https://smarterco.de/spring-data-jpa-query-result-to-dto/

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
	@Query("SELECT new de.smarterco.example.dto.UserNameDTO(u.id, u.name) FROM User u WHERE u.name = :name")
    List<UserNameDTO> retrieveUsernameAsDTO(@Param("name") String name);
}
```

```java

java.io.File dir = new java.io.File("C:\\wrk\\doc\\asi\\clients\\DSIA\\180712-conception\\");
java.io.FileFilter ff = new org.apache.commons.io.filefilter.WildcardFileFilter("DSIA*int*_v0.0.docx");
java.io.File[] files = dir.listFiles(ff);
for(java.io.File f : files) {
	System.out.println(f.getPath());
}
```
