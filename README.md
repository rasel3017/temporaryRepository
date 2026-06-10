generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id         Int        @id @default(autoincrement())
  email      String     @unique
  name       String
  password   String
  role       String     @default("user")
  created_at DateTime   @default(now())
  events     Event[]
  questions  Question[]
  answers    Answer[]
}

model Mosque {
  id         Int      @id @default(autoincrement())
  name       String
  address    String
  region     String
  latitude   Float?
  longitude  Float?
  created_at DateTime @default(now())
  maktabs    Maktab[]
  events     Event[]
}

model Maktab {
  id            Int       @id @default(autoincrement())
  mosque_id     Int
  name          String
  teacher_name  String
  teacher_phone String?
  total_seats   Int?
  created_at    DateTime  @default(now())
  mosque        Mosque    @relation(fields: [mosque_id], references: [id])
  students      Student[]
  fundings      Funding[]
}

model Student {
  id             Int      @id @default(autoincrement())
  maktab_id      Int
  name           String
  age            Int?
  guardian_name  String?
  guardian_phone String?
  enrolled_at    DateTime @default(now())
  maktab         Maktab   @relation(fields: [maktab_id], references: [id])
}

model Funding {
  id         Int      @id @default(autoincrement())
  maktab_id  Int
  donor_name String
  amount     Float
  note       String?
  donated_at DateTime @default(now())
  maktab     Maktab   @relation(fields: [maktab_id], references: [id])
}

model Event {
  id         Int      @id @default(autoincrement())
  mosque_id  Int
  created_by Int
  title      String
  topic      String?
  speaker    String?
  event_date DateTime
  event_time String
  status     String   @default("active")
  created_at DateTime @default(now())
  mosque     Mosque   @relation(fields: [mosque_id], references: [id])
  user       User     @relation(fields: [created_by], references: [id])
}

model Question {
  id         Int      @id @default(autoincrement())
  user_id    Int
  title      String
  body       String
  category   String?
  status     String   @default("open")
  created_at DateTime @default(now())
  user       User     @relation(fields: [user_id], references: [id])
  answers    Answer[]
}

model Answer {
  id          Int      @id @default(autoincrement())
  question_id Int
  user_id     Int
  body        String
  is_accepted Boolean  @default(false)
  created_at  DateTime @default(now())
  question    Question @relation(fields: [question_id], references: [id])
  user        User     @relation(fields: [user_id], references: [id])
}Temporary Repository 
