## Azure DevOps:
##### CI: Continue Integration, should produce artifacts like docker image/acr etc.
- stages - Buid(CI)/Deploy(CD) OR ENV like DEV/TEST/STG/PROD
	- jobs (build, test),Diff platform, job run on agent (from agent pools), runs in parallel
		- template: common reusable pipeline. template: can be for stages, jobs, steps, it can be nested.
		- steps
			- tasks/script, task: pre-configured scripts.
##### CD - Release pipeline: can only be created via UI in ADO
 - its better to CI/CD in single pipeline complete thing, use release only for specific usecase where e.g. Artifacts already avaialable etc.
   
###### Azure -
- `$(Build.SourcesDirectory)` - The local path on the agent where your source code files are downloaded. For example: c:\agent_work\1\s
- `$(System.DefaultWorkingDirectory)`	- The local path on the agent where your source code files are downloaded. For example: c:\agent_work\1\s
- `$(System.ArtifactsDirectory)` - The directory to which artifacts are downloaded during deployment of a release. Example: C:\agent\_work\r1\a
  <br/> The directory is cleared before every deployment if it requires artifacts to be downloaded to the agent.
  <br/> Same as `Agent.ReleaseDirectory` and `System.DefaultWorkingDirectory`

- `$(Build.ArtifactStagingDirectory)` - The local path on the agent where any artifacts are copied to before being pushed to their destination. For example: c:\agent_work\1\a
  <br/> A typical way to use this folder is to publish your build artifacts with the Copy files and Publish build artifacts tasks.

- `$(Agent.BuildDirectory)` - The local path on the agent where all folders for a given build pipeline are created.
  <br/> Same as `Pipeline.Workspace`. For example: /home/vsts/work/1.
- `Pipeline.Workspace` - Workspace directory for a particular pipeline. This variable has the same value as Agent.BuildDirectory. For example, /home/vsts/work/1

###### My learnings:
##### Repo: Have seperate repo for each different kind of projects like frontend/backends so it is easy for pipeline configuration, integration, can run seperately etc.
 
