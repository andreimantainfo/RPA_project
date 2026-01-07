# RPA_project
Setup guide:
1. clone the git repo
2. log into UiStudio with your account
3. open the file Data/Config.xlsx and type in the Settings sheet your UserEmail and UserPassword for the Google account that Google Scholar is linked to
4. make sure your Google Scholar account is fully initialised (add some random publications so you have the metrics this project requires)
5. make sure you are logged out of Google Scholar and log out after every program run (the program assumes you are logged out)
6. run the program in UiStudio - the main workload is in the Process file, where it opens Chrome and logs into the first Google Account in your list of accounts (Scholar doesn't support
   email + password login), then collects its data and puts it in three variables in the Process scope - strI10Index, strHIndex, strCitations
