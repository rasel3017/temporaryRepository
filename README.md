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
