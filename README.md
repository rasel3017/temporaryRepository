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
