           .__                                     
      ____ |  |   ____ _____    ____  __ ________  
    _/ ___\|  | _/ __ \\__  \  /    \|  |  \____ \ 
    \  \___|  |_\  ___/ / __ \|   |  \  |  /  |_> >
     \___  >____/\___  >____  /___|  /____/|   __/ 
         \/          \/     \/     \/      |__|    
                   .__.__       .___.__            
      _____ _____  |__|  |    __| _/|__|______     
     /     \\__  \ |  |  |   / __ | |  \_  __ \    
    |  Y Y  \/ __ \|  |  |__/ /_/ | |  ||  | \/    
    |__|_|  (____  /__|____/\____ | |__||__|       
          \/     \/              \/                

### USAGE
  cleanup-maildir [OPTION].. COMMAND FOLDERNAME..

### DESCRIPTION
  Cleans up old messages in FOLDERNAME; the exact action taken
  depends on COMMAND. Multiple FOLDERNAMEs or GLOB patterns are
  allowed. Be aware that there is no filter for duplicates.

### COMMANDS
* archive - move old messages to destination folder
* delete! - permanently delete old messages (will be gone forever!)

### OPTIONS
##### -h, --help
    Show this help.  
##### -q, --quiet
    Suppress normal output.
##### -v, --verbose
    Output extra information for testing.
##### -d, --dry-run
    Do not actually touch any files; just say what would be done.
##### -n, --keep-new
    Do not touch messages that are flagged as unread or new.
##### -t, --keep-threads
    Do not touch messages if any message in this thread is flagged.
      
    Note: the thread-detection mechanism is currently based purely on
    a message's subject. The In-Reply-To header is not observed yet.
##### --age=N
    Only touch messages older than N days. Default is 365 days.
##### --dest=F
    Path to destination maildir folder. Default is './Archive/%y/%m'.

    The following patterns will be substituted:
    • `%y` - year (e.g. 2018)
    • `%m` - month (e.g. 01 to 12)
    • `%d` - day (e.g. 01 to 31)
    • `%f` - folder name of this mail
    • `%%` - replaced by a single percent sign

### EXAMPLES
Archive messages from Sent and all INBOX folders after 90 days:
  
    cleanup-maildir --age=90 --dest=./Archive/%f archive ./Sent ./INBOX*

Delete over 1 year old message in 'Lists/debian-devel' folder, except messages that are flagged as unread:
  
    cleanup-maildir --keep-new delete! './Lists.debian-devel'
