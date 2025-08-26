Due to an accidental data mix-up, user data was unintentionally mingled on Nautilus App Server 3 at the /home/usersdata location by the Nautilus production support team in Stratos DC. To rectify this, specific user data needs to be filtered and relocated. Here are the details:



Locate all files (excluding directories) owned by user anita within the /home/usersdata directory on App Server 3. Copy these files while preserving the directory structure to the /official directory.


    ```bash
    ssh banner@stapp03.stratos.xfusioncorp.com

    # -type f ensures only files are selected, excluding directories
    # --parents option preserves the directory structure
    # -exec option allows executing a command on the found files
    # In this case, we are using cp to copy the files to the /official directory
    # -exec cp --parents {} /official \; will copy each found file while preserving the directory structure
    sudo find /home/usersdata -user anita -type f -exec cp --parents \{\} /official \;

    # verify
    sudo ls /official
    # check the copied files
    sudo find /official -user anita -type f
    # we should see the copied files listed here
