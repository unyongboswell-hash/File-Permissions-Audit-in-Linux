# File-Permissions-Audit-in-Linux
Managed file and directory access controls using Bash commands to enforce the Principle of Least Privilege.


## Project Overview

Secured an organization's sensitive research directory (`/projects`) by auditing existing file access and modifying Linux permissions (`chmod`) to enforce the Principle of Least Privilege. This project involved identifying permission gaps, removing unauthorized write/execute access, and hardening hidden configuration files.

## Technologies Used
* **OS**: Linux (Ubuntu/Debian environment)
* **Commands**: `ls -la`, `chmod` (symbolic mode)

 ## Key Actions & Linux Implementations
  ### 1. Directory Audit & Analysis
   * Used `ls -la` to inspect permissions across standard files, directories, and hidden files (e.g., `.project_x.txt`).
   * Analyzed the 10-character permission string (`d|rwx|rwx|rwx`) to map access levels across User, Group, and Other.
  ### 2. Restricting Public Access (`Other`)
   * **Problem**: Standard project files had active write access for unauthenticated system users (`other`).
   * **Solution**: Stripped write access from the public tier to prevent unauthorized data tampering.
   *  **Command:**
`chmod o-w project_k.txt`
  ### 3. Hardening Archived & Hidden Files
  * **Problem:** A sensitive archived file (`.project_x.txt`) retained active write privileges.
  * **Solution:** Locked down the file to read-only status for authorized team members while revoking user/group modification rights.
  * **Command:**
`chmod u-w,g-w,g+r .project_x.txt`
  ### 4. Securing Directory Traversal (Execute Rights)
  * **Problem:** The sensitive `/draft`s directory allowed group-level execution, creating a data leak risk.
  * **Solution:** Revoked group execute rights to ensure only the primary owner (`researcher2`) could enter and access the directory contents.
  * **Command:**
  `chmod g-x drafts/`
## Business Outcomes & Key Takeaways
  * **Enforced Least Privilege:** Restructured system access so users only possess the exact permissions required for their roles.
  *  **Data Integrity:** Prevented accidental or malicious modification of archived research data.
  *  **System Hardening:** Eliminated lateral directory traversal risks by restricting execution rights on sensitive folders.
