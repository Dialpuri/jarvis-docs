# Jarvis

## Connecting to Jarvis

Once you have a user account setup you can connect to jarvis using the following command in a terminal. 

	ssh <username>@jarvis.chem.york.ac.uk

It will prompt you to enter your password and after you should be met with a terminal screen which looks similar to this 

	username@jarvis:~$  

## Running a job using Slurm

Slurm is an open source cluster management and job scheduling system for  Linux clusters. This allows you to queue jobs which will run when the system has enough resources to fulfil your request. It is discouraged to run jobs without the use of Slurm.

### Job file configuration

Create a new file with the .job suffix which contains the following information. 

#### Single threaded 
~~~bash
#!/bin/bash
#SBATCH --job-name=basic_job_test        # Job name
#SBATCH --ntasks=1                       # Run on a single CPU
#SBATCH --mem=1gb                        # Job memory request
#SBATCH --time=00:05:00                  # Time limit hrs:min:sec
#SBATCH --output=basic_job_%j.log        # Standard output and error log
 
echo My working directory is `pwd`
echo Running job on host:
echo -e '\t'`hostname` at `date`
echo
 
COMMANDS YOU WOULD RUN IN TERMINAL HERE
  
echo
echo Job completed at `date`
~~~

#### Multi-threaded 
~~~bash
#!/bin/bash
#SBATCH --job-name=basic_job_test        # Job name
#SBATCH --ntasks=1                       # Run on a single CPU
#SBATCH --cpus-per-task=4 			  	 # ...with four cores`
#SBATCH --mem=1gb                        # Job memory request
#SBATCH --time=00:05:00                  # Time limit hrs:min:sec
#SBATCH --output=threaded_job_%j.log        # Standard output and error log
 
echo My working directory is `pwd`
echo Running job on host:
echo -e '\t'`hostname` at `date`
echo
 
COMMANDS YOU WOULD RUN IN TERMINAL HERE
    
echo
echo Job completed at `date`
~~~

### Checking job status

To check job status simply run the following command 
	
	squeue

If you would like to filter to jobs only you have started use the --u flag
	
	squeue -u <username> 
