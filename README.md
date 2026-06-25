model Mosque {
  id          String   @id @default(uuid())
  name        String
  address     String
  region      String
  latitude    Float?
  longitude   Float?
  imamName    String?
  muazzinName String?
  imageUrl    String?
  fajrTime    String?
  zuhrTime    String?
  asrTime     String?
  maghribTime String?
  ishaTime    String?
  userId      String
  user        User     @relation(fields: [userId], references: [id])
  maktabs     Maktab[]
  events      Event[]
}

model Maktab {
  id             String    @id @default(uuid())
  name           String
  address        String?
  teacherName    String
  teacherPhone   String
  totalSeats     Int
  coursesOffered String?
  imageUrl       String?
  mosqueId       String?
  mosque         Mosque?   @relation(fields: [mosqueId], references: [id])
  students       Student[]
  fundings       Funding[]
}

model Event {
  id          String   @id @default(uuid())
  title       String
  topic       String
  speaker     String
  eventDate   DateTime
  eventTime   String
  location    String?
  description String?
  imageUrl    String?
  isFree      Boolean  @default(true)
  status      String   @default("upcoming")
  mosqueId    String
  mosque      Mosque   @relation(fields: [mosqueId], references: [id])
}
