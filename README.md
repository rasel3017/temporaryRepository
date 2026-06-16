model Mosque {
  id        String   @id @default(uuid())
  name      String
  address   String
  region    String
  latitude  Float?
  longitude Float?

  maktabs   Maktab[]
  events    Event[]
}
