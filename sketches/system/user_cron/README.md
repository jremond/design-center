# cfdc_user_cron - Manage user cron files
## AUTHOR
Jean Remond <cfengine@remond.re>

## PLATFORM
linux

## DESCRIPTION
* cfdc_user_cron
    - edit_line based
    - optionally removes any cron not specified 


## REQUIREMENTS
standard library

## SAMPLE USAGE
    body common control
    {
          bundlesequence => { "test" };
          inputs => { "../../libraries/copbl/cfengine_stdlib.cf", "main.cf", };
    }
    
    bundle common cfsketch_g
    {
      vars:
           "user_cron_defined_only"                 string => "no";
           "user_cron_prefix_file"                  string => "/tmp/cron_";
           "user_cron_cron[cron_1][command]"        string => "/bin/echo cron_1 > /dev/null 2>&1";
           "user_cron_cron[cron_1][day_of_month]"   string => "1";
           "user_cron_cron[cron_1][day_of_week]"    string => "*";
           "user_cron_cron[cron_1][hour]"           string => "*";
           "user_cron_cron[cron_1][minute]"         string => "*";
           "user_cron_cron[cron_1][month]"          string => "6";
           "user_cron_cron[cron_1][user]"           string => "root";
    
    }
    
    bundle agent test
    {
      methods:
          "any" usebundle => cfdc_user_cron("cfsketch_g.user_cron_");
    
    }