# LIGO practical intro doc

Some useful links for registering to LVK and test-runs of GWs events.



## Step 1: Become a LIGO member

- Register for a LIGO membership [here](https://my.ligo.org/).

After your membership is accepted:

- Register for LIGO's Mattermost [here](https://chat.ligo.org/). 

  Many channels are open for joining $\rightarrow$ you can find them by clicking the $+$ sign, next to `LIGO` at the top-left. This will open a list of available public channels (beware, the list continues for multiple pages - click `Next` at bottom-right, to check them all).
  

- Apply for a LIGO cluster account [here](https://ldg.ligo.org/ldg/manage/).
  

- Create a GitLab LIGO account [here](https://git.ligo.org/).



## Step 2: Background for GWs analysis

- The GWs Open Data Workshops [(here)](https://gwosc.org/workshops/) are very useful to understand the basics of GWs analysis. There is also a dedicated forum ([here](https://ask.igwn.org/)) with Q&A about the workshops, but also more general issues.

- The IGWN Public Alerts page ([here](https://emfollow.docs.ligo.org/userguide/)) has a very useful website describing the whole process, but also many of the relevant [terminology](https://emfollow.docs.ligo.org/userguide/glossary.html).

  

## Step 3: LIGO Observing runs

- A useful compilation of FAQ can be found [here](https://git.ligo.org/pe/O4/o4a-rota/-/wikis/FAQs).

- A quick tutorial, using `bilby` to analyse, i.e. do a parameter estimation (PE), of a GW event is [here](https://git.ligo.org/pe/O4/o4a-rota/-/wikis/quick-bilby-tutorials). Beware that there could be some typos on the event's naming, so try to be consistent with the original event's naming at the top, i.e. the command that creates the `bilby` configuration file.

  

- The general idea is the following: 

  	1. We create a directory for the PE run
  	1. Activate relevant python environments
  	1. Make all the necessary (physical) changes in the `filename_config.ini`
  	1. Secure permission (If problems with permission occur, check [(here)](https://computing.docs.ligo.org/guide/auth/kerberos/) for alternative authorisation options. Sometimes the error log files of a failed job can have useful links.)
  	1. Run the analysis: `bilby_pipe filename_config.ini --submit`
   	6. Check analysis: `condor_q --nobatch`. More on `HTCondor` workload manager [here](https://computing.docs.ligo.org/guide/htcondor/).
       

- More details on `bilby` configuration options can be found [here](https://lscsoft.docs.ligo.org/bilby_pipe/1.0.1/index.html). 
  - For user-interface, i.e. options in the config file, check [here](https://lscsoft.docs.ligo.org/bilby_pipe/1.0.1/user-interface.html).
  - `Bilby` can be used to create a configuration `.ini` file based on _GraceDB_ events. For a specific example [(here)](https://git.ligo.org/pe/O4/o4a-rota/-/issues/66#note_821020) and more generally [(here)](https://lscsoft.docs.ligo.org/bilby_pipe/1.0.1/examples.html#running-on-gracedb-events).
  - __Note__: There is a dedicated channel in LIGO mattermost (_Bilby Help_) for issues with `bilby`.



- __Where to run?__

  

  To access the LIGO clusters, follow the ways [here](https://computing.docs.ligo.org/guide/computing-centres/ldg/#access-ldg). For UNLV GWs group, we use the _CIT_ site, with the following hosts:

  

  <img src="C:\Users\klera\Documents\GitHub\LIGO_intro\LIGO_system.png" alt="image" style="zoom:60%;" />

LIGO has a number of workstations - the `HTCondor` system will distribute the run accordingly. The `ldas-grid` and `ldas-pcdev*` are good for hosting your files and analyses (check the system configuration, in case you are interested in a job with specific characteristics, like high memory etc).



## Step 4: Checking your `bilby` runs' results

Of course, the files could be downloaded and inspected locally. But there is also the possibility to examine some of the plots online:

- Follow the links [here](https://computing.docs.ligo.org/guide/computing-centres/cit/#additional-services). Either `Jupytel Lab` or the `public_html` page organise the produced plots.

- To create a summary webpage (shown in `public_html` above), the following options must be selected in the configuration file:

  ```
  create-summary = True
  email = albert.einstein@ligo.org
  webdir = /home/albert.einstein/public_html/project
  ```

- The `dag_name.submit` file and `bash_name.sh` file have useful information on the order of jobs submissions, but also on the commands used at each step that initialise the specific part of the run (these can be useful, if you want to check)

