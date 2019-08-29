# utl-creating-tables-at-macro-execution-time
Creating tables at macro execution time  
    Creating tables at macro execution time                                                                                 
                                                                                                                            
    Is this what you want?                                                                                                  
                                                                                                                            
    github                                                                                                                  
    https://tinyurl.com/y3tvk4mo                                                                                            
    https://github.com/rogerjdeangelis/utl-creating-tables-at-macro-execution-time                                          
                                                                                                                            
    https://tinyurl.com/y5ysdacw                                                                                            
    https://communities.sas.com/t5/SAS-Programming/Output-is-showing-in-log-but-want-in-sas-dataset-format/m-p/584896       
                                                                                                                            
                                                                                                                            
    https://tinyurl.com/yaajbg36                                                                                            
    https://github.com/rogerjdeangelis/utl_file_and_directory_utilities_for_all_operating_systems                           
                                                                                                                            
    *_                   _                                                                                                  
    (_)_ __  _ __  _   _| |_                                                                                                
    | | '_ \| '_ \| | | | __|                                                                                               
    | | | | | |_) | |_| | |_                                                                                                
    |_|_| |_| .__/ \__,_|\__|                                                                                               
            |_|                                                                                                             
    ;                                                                                                                       
                                                                                                                            
    * ceate a directory and some files;                                                                                     
    data _null_;                                                                                                            
                                                                                                                            
      * create directory;                                                                                                   
      if _n_=0 then do;                                                                                                     
          %let rc=%sysfunc(dosubl('                                                                                         
             data _null_;                                                                                                   
                 rc=dcreate("hom","d:/");                                                                                   
             run;quit;                                                                                                      
         '));                                                                                                               
      end;                                                                                                                  
                                                                                                                            
      file "d:/hom/file1.hom"; put "file1";                                                                                 
      file "d:/hom/file2.hom"; put "file2";                                                                                 
      file "d:/hom/file3.hom"; put "file3";                                                                                 
                                                                                                                            
    run;quit;                                                                                                               
                                                                                                                            
     d:/hom                                                                                                                 
       /file1.hom                                                                                                           
       /file2.hom                                                                                                           
       /file3.hom                                                                                                           
                                                                                                                            
                                                                                                                            
    *            _               _                                                                                          
      ___  _   _| |_ _ __  _   _| |_                                                                                        
     / _ \| | | | __| '_ \| | | | __|                                                                                       
    | (_) | |_| | |_| |_) | |_| | |_                                                                                        
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                       
                    |_|                                                                                                     
    ;                                                                                                                       
                                                                                                                            
    Up to 40 obs from FILELIST total obs=3                                                                                  
                                                                                                                            
                                  NUMBER_OF_    MEMBER_                                                                     
    Obs     PTH      FILENAME       MEMBERS      NUMBER                                                                     
                                                                                                                            
     1     d:/hom    file1.hom         3           1                                                                        
     2     d:/hom    file2.hom         3           2                                                                        
     3     d:/hom    file3.hom         3           3                                                                        
                                                                                                                            
                                                                                                                            
    *          _       _   _                                                                                                
     ___  ___ | |_   _| |_(_) ___  _ __  ___                                                                                
    / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|                                                                               
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                                               
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/                                                                               
                                                                                                                            
                                                                                                                            
                                                                                                                            
    %macro utl_dir(pth,out);                                                                                                
                                                                                                                            
       %let rc=%sysfunc(dosubl('                                                                                            
                                                                                                                            
         data &out(drop=rc did i);                                                                                          
           retain pth filename number_of_members filename member_number;                                                    
           rc=filename("mydir","&pth");                                                                                     
           did=dopen("mydir");                                                                                              
           if did > 0 then do;                                                                                              
              number_of_members=dnum(did);                                                                                  
              do i=1 to number_of_members;                                                                                  
                filename=dread(did,i);                                                                                      
                member_number+1;                                                                                            
                pth="&pth";                                                                                                 
                output;                                                                                                     
             end;                                                                                                           
          end;                                                                                                              
        run;quit;                                                                                                           
                                                                                                                            
        '));                                                                                                                
                                                                                                                            
    %mend utl_dir;                                                                                                          
                                                                                                                            
    %utl_dir(d:/hom,filelist);                                                                                              
                                                                                                                            
                                                                                                                            
