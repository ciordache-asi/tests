# tests
tests repo
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
  
---------------------------------------

Exemple @Query mapping to DTO : https://stackoverflow.com/a/36109273

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
