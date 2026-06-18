PS C:\DBMS_PROJECT\Smart_Mosque_Management> npx prisma migrate dev --name add_userId_to_mosque
Loaded Prisma config from prisma.config.ts.

Prisma schema loaded from prisma\schema.prisma.
Datasource "db": PostgreSQL database "smart_mosque_db", schema "public" at "localhost:5432"


Error: 
⚠️ We found changes that cannot be executed:

  • Step 0 Added the required column `userId` to the `Mosque` table without a default value. There are 1 rows in this table, it is not possible to execute this step.

You can use prisma migrate dev --create-only to create the migration file, and manually modify it to address the underlying issue(s).
Then run prisma migrate dev to apply it and verify it works.

PS C:\DBMS_PROJECT\Smart_Mosque_Management> 
