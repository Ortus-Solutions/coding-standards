[&lt;&lt; Back to Dashboard]

|             |
|-------------|
| \_\_TOC\_\_ |

Database Naming Conventions
===========================

A naming convention is important when working with databases in order to provide a clear structure and format; especially in team environments. By using these conventions the database can be understood by anyone applying these conventions; thus increasing maintainability. These are not rules but guidelines that can be adapted to any working environment.

General Conventions
-------------------

-   All names should be in camelcase with the first letter in lower case.

<!-- -->

    -- DO THIS --
    user
    permision
    userPermission

    -- NOT THIS --
    User
    Permission
    User_Permission
    user_permission

-   Separate name parts by using camel case and NOT underscores or spaces. This provides better readibility and you will not have to use quotes when doing SQL statements. Look at example in the previous point.
-   Prefixes or namespaces are the ONLY parts of names that should be separated by underscores. This defines a clear separation between names and areas.

<!-- -->

     -- DO THIS --
     blog_user
     blog_userPermission
     
     -- NOT THIS --
     BlogUser
     BlogUserPermission
     Blog_UserPermission

-   Do not use numbers in names. This is poor design, indicating divided table structures.
-   Do not use dot (.) separator between names, remember use camel casing. This way you will avoid problems whend doing SQL statements as fields are accessed using dot notation.
-   It goes without saying, do not use reserved database words in any name.
-   Always try to use names that make sense and are descriptive of their purpose.
-   Avoid abbreviations whenever possible. ONLY use abbreviations that are well known and documented.
-   Avoid acronyms whenever possible. Only use acronyms that are well known and documented. Also, they should all be in uppercase if used.

<!-- -->

    -- DO THIS --
    HTTPRequests
    savedURL

    -- NOT THIS --
    http_requests
    httprequests
    savedurl
    saved_url

Table Conventions
-----------------

-   Tables are usually entity you are modeling for persistence. So make sure the names are in proper English and carry natural meanings. These names should make sense and should be descriptive.
-   Avoid acronyms and abbreviations if at all possible. If acronyms are used, then make sure to capitalize them. Abbreviations used should be well known abbreviations and should be camel cased.
-   Avoid using plural names for tables, use singular forms. This will avoid errors due to pluralization of words and also when moving table design to objects or entities. The name should map to the entity it is modeling.

<!-- -->

    -- DO THIS --
    blog_user
    blog_page
    person
    box
    activity

    -- NOT THIS --
    blog_users
    blog_pages
    people
    boxes
    activities

-   Use namespaces for tables whenever grouping is needed. This grouping is a clear separation when working with the tables and can also provide a good basis for security, as you could secure via the namespace. Namespaces should be separated by an

  [&lt;&lt; Back to Dashboard]: Dashboard "wikilink"