#Change Logs
Provide logs of terminal output/tests with date & time stamps to note progress/changes/concerns

2/28/19 4:29 PM

   * _**NOTE:**_ All commands have pre-populated cache data as needed, due to current lack of connection to cache server. **THIS WILL CHANGE**
    
   - [x] All commands show in help menu
   - [x] `Put` command message shows success
   - [ ] `Read` command still fails
   - [x] `Update` command works
   - [x] `Delete` command works
       
        _**COMMENT**_ currently using terminal as intermediate test harness. Unit/Integration tests next after commands all work in terminal.
    
       ```
        richm :~/gocode/src/CacheCLI :[thurs-new-cli !] go build -o cli
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli put name ducati
           put success:  cache '&{map[name:ducati]}' 
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli update kitten Benny
           update success:  cache '&{map[name:harley animal:horse kitten:Benny]}' 
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli read kitten
           [kitten] 1
           
           read failed: key 'kitten' invalid or cache empty
           Error: read failed: key 'kitten' invalid or cache empty
           Usage:
             cli read [flags]
           
           Flags:
             -h, --help   help for read
           
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli delete animal
           delete success: cache '&{map[name:harley kitten:Bene]}' 
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli help
           Usage:
             cli [command]
           
           Available Commands:
             delete      delete key-value pair
             help        Help about any command
             put         put key-value pair
             read        read given key and return value
             update      update key-value pair
           
           Flags:
             -h, --help   help for cli
           
           Use "cli [command] --help" for more information about a command.
       ```
       
2/28/19 4:47 PM

   * _**NOTE:**_ All commands have pre-populated cache data as needed, due to current lack of connection to cache server. **THIS WILL CHANGE**
    
   - [x] All commands show in help menu
   - [x] Put command message shows success
   - [x] Read command still fails
   - [x] Update command works
   - [x] Delete command works
    
   * _**COMMENT**_ currently using terminal as intermediate test harness. Unit/Integration tests next after commands all work in terminal.
    
   * PROOF OF WORKING COMMANDS BELOW
    
       ```
        srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] go build -o cli
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli help
           Usage:
             cli [command]
           
           Available Commands:
             delete      delete key-value pair
             help        Help about any command
             put         put key-value pair
             read        read given key and return value
             update      update key-value pair
           
           Flags:
             -h, --help   help for cli
           
           Use "cli [command] --help" for more information about a command.
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli put kitten harley
           put success:  cache '&{map[kitten:harley]}' 
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli read kitten
           [kitten] 1
           <nil>
           >> Bene
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli update kitten ducati
           update success:  cache '&{map[animal:horse kitten:ducati name:harley]}' 
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli delete horse
           delete failed: key 'horse' not in cache
           Error: delete fail
           Usage:
             cli delete [flags]
           
           Flags:
             -h, --help   help for delete
           
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli delete animal
           delete success: cache '&{map[name:harley kitten:Bene]}'
       ```

2/28/19 5:15 PM

Tests of `put` terminal commands in terminal.
     
   - [ ] `put` terminal command doesn't fail as expected when trying to put for existing key value (BOOO)
     
        ```
           srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] go build -o cli
            srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli put name Bonny
            put success:  cache '&{map[name:Bonny animal:horse kitten:Bene]}' 
            srichm :~/gocode/src/CacheCLI :[thurs-new-cli !]   ```
            

  - [x] `put` terminal command works as expected when given empty string inputs for either key or value
 
    ```srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli put name
       Error: requires at least 2 arg(s), only received 1
       Usage:
         cli put [flags]
       
       Flags:
         -h, --help   help for put
       
       srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli put  
       Error: requires at least 2 arg(s), only received 0
       Usage:
         cli put [flags]
       
       Flags:
         -h, --help   help for put
       
       srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli put  betty
       Error: requires at least 2 arg(s), only received 1
       Usage:
         cli put [flags]
       
       Flags:
         -h, --help   help for put
    ```
    
  - [x] `put` terminal command works for putting key value pair into cache 
    
    ```srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli put name Bonny
       put success:  cache '&{map[name:Bonny animal:horse kitten:Bene]}'
       ./cli put dog frankie
       put success:  cache '&{map[name:harley animal:horse kitten:Bene dog:frankie]}' 
       ```

2/29/19 5:40 PM

 * Tests of `Read` terminal commands in terminal. 
 - [x] Errors correctly for empty strings
 
     ``` ./cli read
        Error: requires at least 1 arg(s), only received 0
        Usage:
          cli read [flags]
        
        Flags:
          -h, --help   help for read
    ```
 - [x] Works correctly to `read` value given key to data in pre-populated cache. Current hard-coded working keys are `animal`, `name` and `kitten`
 
      ```srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli read animal
         >> value for key is:  horse
         srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli read name
         >> value for key is:  harley
    ```

 - [x] Errors correctly when given invalid `key`
    ```srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli read book
       Error: read failed: key 'book' invalid or cache empty
       Usage:
         cli read [flags]
       
       Flags:
         -h, --help   help for read
       
    ```
 - [ ] Future CLI feature could have note if extra args return message like "I notice extra words in your read command, did you mean to put or update a key value pair instead of read?"
   
    ```srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli read animal harley
       >> value for key is:  horse
       
     ```

2/28/19 6:11 PM
Tests for `update` command in terminal.
 - [x] Errors correctly for empty strings/incomplete args
 
    ``` ./cli update
       Error: requires at least 2 arg(s), only received 0
       Usage:
         cli update [flags]
       
       Flags:
         -h, --help   help for update
       
       srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli update name
       Error: requires at least 2 arg(s), only received 1
       Usage:
         cli update [flags]
       
       Flags:
         -h, --help   help for update
       
       srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli update  name 
       Error: requires at least 2 arg(s), only received 1
       Usage:
         cli update [flags]
       
       Flags:
         -h, --help   help for update
       
    ```
  - [x] Works correctly for updating when passed valid (existing in pre-populated cache) `key`
  
    ```srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli update name Ducati
       update success:  cache '&{map[animal:horse kitten:Bene name:Ducati]}' 
    ```
  - [x] Errors correctly when given invalid key/value pair
    ```./cli update read book
       update failed: key 'read' not in cache
       Error: 
       Usage:
         cli update [flags]
       
       Flags:
         -h, --help   help for update
    ```
 2/28/19 6:21 PM Tests for `delete` command in terminal.
 
 - [x] Errors correctly when given invalid key
    ```srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli delete book
       delete failed: key 'book' not in cache
       Error: 
       Usage:
         cli delete [flags]
       
       Flags:
         -h, --help   help for delete
     ```
 - [x] Errors correctly when given empty string as key
    ```srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli delete 
       Error: requires at least 1 arg(s), only received 0
       Usage:
         cli delete [flags]
       
       Flags:
         -h, --help   help for delete
       
    ```
 - [x] Works correctly when given valid key to remove both key and value from cache (prepopulated)
    ```
    srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] ./cli delete animal
    delete success: cache '&{map[name:harley kitten:Bene]}' 
    srichm :~/gocode/src/CacheCLI :[thurs-new-cli !] 
    ```

3/1/19

_**NOTE**_ : *`put`* method refactored to *`create`*

3/4/19 3:09 PM
 
 -[x] MockKVCache and associate implementation of Mock methods created in KVCache file
 -[x] CommandRunner struct created to run either MockKVCache or SimpleKVCache for both test and production implementations of the `kvc` CLI application
 -[x] CreateCmd abstracted away from root.go command file
 -[x] Unit test for MockKVCache pass
 -[x] Unit tests for CreateCommand pass
 -[x] Terminal as test harness tests pass for CreateCommand
 
   ```srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] go build -o kvc
      srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc create good book
      &{map[name:harley animal:horse kitten:Bene]}
      create success:  cache '&{map[name:harley animal:horse kitten:Bene good:book]}' 
      srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc create book
      Error: requires at least 2 arg(s), only received 1
      Usage:
        cli create [flags]
      
      Flags:
        -h, --help   help for create
      
      srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc create
      Error: requires at least 2 arg(s), only received 0
      Usage:
        cli create [flags]
      
      Flags:
        -h, --help   help for create
      
      srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] 
    ``` 
3/4/19 4:18 PM

  -[x] ReadCmd abstracted away from root.go command file
  -[x] Unit tests for ReadCmd pass
  -[x] Terminal as test harness tests pass for ReadCmd
  
    ```srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] go build -o kvc
     srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc create book dracula
     create success:  cache '&{map[name:harley animal:horse kitten:Bene book:dracula]}' 
     srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc read name
     >> value for key is:  harley
     srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc create book
     Error: requires at least 2 arg(s), only received 1
     Usage:
       kvc create [flags]
     
     Flags:
       -h, --help   help for create
     
     srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc read
     Error: requires at least 1 arg(s), only received 0
     Usage:
       kvc read [flags]
     
     Flags:
       -h, --help   help for read
     
     srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc read book
     Error: read failed: key 'book' invalid or cache empty
     Usage:
       kvc read [flags]
     
     Flags:
       -h, --help   help for read
     
     srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] 
    ```
3/4/19 5:11 PM

  -[x] UpdateCmd abstracted away from root.go command file
  -[x] Unit tests for UpdateCmd pass
  -[x] Terminal as test harness tests pass for UpdateCmd

    ```srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] go build -o kvc
       srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc create book crafty
       create success:  cache '&{map[name:harley animal:horse kitten:Bene book:crafty]}' 
       srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc create book
       Error: requires at least 2 arg(s), only received 1
       Usage:
         kvc create [flags]
       
       Flags:
         -h, --help   help for create
       
       srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc update kitten Zuki
       update success:  cache '&{map[name:harley animal:horse kitten:Zuki]}' 
       srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc read name
       >> value for key is:  harley
       srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc read 
       Error: requires at least 1 arg(s), only received 0
       Usage:
         kvc read [flags]
       
       Flags:
         -h, --help   help for read
       
       srichm :~/gocode/src/CacheCLI :[mon-cli-test !?] ./kvc update kitten
       Error: requires at least 2 arg(s), only received 1
       Usage:
         kvc update [flags]
       
       Flags:
         -h, --help   help for update
    ```

3/5/19 - all day - updating tests to get to close as 100% coverage as possible in both cmd and kvcache packages. 

3/6/19 - wrote server and server unit tests

3/7 - 8/19 - refining server unit tests, working on mock server cache improving test coverage

3/11 - 12/19 - refactoring code and tests for efficiency

3/13/19 - wrote client, started client unit tests

3/14/19 - completed client unit tests, completed manual client/server terminal tests, code cleanup, documentation 
refinement, go fmt confirmation, etc.