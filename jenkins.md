# Jenkins knowledge

## Tricks
- **How to exclude a file or folder from SVN monitoring in Jenkins build?**
    - In your **Job Configuration**, under **Source Code Management** section, click the **Advanced...** button.
    - This opens up **Excluded Regions** field. Click the question **?** icon next to it for more information. Add the excluded region as:
        > /exclude-folder/.*
        
    - **Note**: The pattern is relative from the **root of your repo**