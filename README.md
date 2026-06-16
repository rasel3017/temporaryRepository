model Maktab {
  id           String   @id @default(uuid())
  name         String
  teacherName  String
  teacherPhone String
  totalSeats   Int
  mosqueId     String

  mosque       Mosque    @relation(fields: [mosqueId], references: [id])
  students     Student[]
  fundings     Funding[]
}


model Student {
  id            String   @id @default(uuid())
  name          String
  age           Int
  guardianName  String
  guardianPhone String
  enrolledAt    DateTime @default(now())
  maktabId      String

  maktab        Maktab   @relation(fields: [maktabId], references: [id])
}


model Funding {
  id         String   @id @default(uuid())
  donorName  String
  amount     Float
  note       String?
  donatedAt  DateTime @default(now())
  maktabId   String

  maktab     Maktab   @relation(fields: [maktabId], references: [id])
}


model Event {
  id        String   @id @default(uuid())
  title     String
  topic     String
  speaker   String
  eventDate DateTime
  eventTime String
  status    String   @default("upcoming")
  mosqueId  String

  mosque    Mosque   @relation(fields: [mosqueId], references: [id])
}


model Question {
  id        String   @id @default(uuid())
  title     String
  body      String
  category  String
  status    String   @default("open")
  createdAt DateTime @default(now())
  userId    String

  user      User     @relation(fields: [userId], references: [id])
  answers   Answer[]
}


model Answer {
  id         String   @id @default(uuid())
  body       String
  isAccepted Boolean  @default(false)
  createdAt  DateTime @default(now())
  userId     String
  questionId String

  user       User     @relation(fields: [userId], references: [id])
  question   Question @relation(fields: [questionId], references: [id])
}
