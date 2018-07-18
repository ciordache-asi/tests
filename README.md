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
