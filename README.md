model Funding {
  id        String   @id @default(uuid())
  donorName String
  amount    Float
  note      String?
  donatedAt DateTime @default(now())
  maktabId  String?
  mosqueId  String?
  maktab    Maktab?  @relation(fields: [maktabId], references: [id])
  mosque    Mosque?  @relation(fields: [mosqueId], references: [id])
}
