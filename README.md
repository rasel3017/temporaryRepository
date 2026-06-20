import { PrismaClient } from "../src/generated/prisma/client.js";
import { PrismaPg } from "@prisma/adapter-pg";
import bcrypt from "bcryptjs";
import dotenv from "dotenv";

dotenv.config();

const adapter = new PrismaPg({
  connectionString: process.env.DATABASE_URL,
});

const prisma = new PrismaClient({ adapter });

async function main() {
  console.log("Seeding database...");

  // Create admin user
  const hashedPassword = await bcrypt.hash("admin123", 12);
  const userPassword = await bcrypt.hash("user123", 12);

  const admin = await prisma.user.upsert({
    where: { email: "admin@mosque.com" },
    update: {},
    create: {
      name: "Admin",
      email: "admin@mosque.com",
      password: hashedPassword,
      role: "admin",
    },
  });

  const user1 = await prisma.user.upsert({
    where: { email: "rasel@gmail.com" },
    update: {},
    create: {
      name: "Rasel Ahmed",
      email: "rasel@gmail.com",
      password: userPassword,
      role: "user",
    },
  });

  const user2 = await prisma.user.upsert({
    where: { email: "karim@gmail.com" },
    update: {},
    create: {
      name: "Abdul Karim",
      email: "karim@gmail.com",
      password: userPassword,
      role: "user",
    },
  });

  console.log("Users created ✅");

  // Create mosques
  const mosque1 = await prisma.mosque.upsert({
    where: { id: "seed-mosque-001" },
    update: {},
    create: {
      id: "seed-mosque-001",
      name: "Baitul Mukarram",
      address: "Topkhana Road, Dhaka",
      region: "Dhaka",
      latitude: 23.7275,
      longitude: 90.4099,
      userId: admin.id,
    },
  });

  const mosque2 = await prisma.mosque.upsert({
    where: { id: "seed-mosque-002" },
    update: {},
    create: {
      id: "seed-mosque-002",
      name: "Star Mosque",
      address: "Armanitola, Old Dhaka",
      region: "Dhaka",
      latitude: 23.7104,
      longitude: 90.4074,
      userId: admin.id,
    },
  });

  const mosque3 = await prisma.mosque.upsert({
    where: { id: "seed-mosque-003" },
    update: {},
    create: {
      id: "seed-mosque-003",
      name: "Shahi Jame Mosque",
      address: "Rajshahi City",
      region: "Rajshahi",
      latitude: 24.3745,
      longitude: 88.6042,
      userId: admin.id,
    },
  });

  const mosque4 = await prisma.mosque.upsert({
    where: { id: "seed-mosque-004" },
    update: {},
    create: {
      id: "seed-mosque-004",
      name: "Sixty Dome Mosque",
      address: "Bagerhat",
      region: "Khulna",
      latitude: 22.6602,
      longitude: 89.7304,
      userId: admin.id,
    },
  });

  console.log("Mosques created ✅");

  // Create maktabs
  const maktab1 = await prisma.maktab.upsert({
    where: { id: "seed-maktab-001" },
    update: {},
    create: {
      id: "seed-maktab-001",
      name: "Baitul Mukarram Maktab",
      teacherName: "Maulana Abdul Karim",
      teacherPhone: "01712345678",
      totalSeats: 50,
      mosqueId: mosque1.id,
    },
  });

  const maktab2 = await prisma.maktab.upsert({
    where: { id: "seed-maktab-002" },
    update: {},
    create: {
      id: "seed-maktab-002",
      name: "Star Mosque Maktab",
      teacherName: "Maulana Ibrahim",
      teacherPhone: "01812345678",
      totalSeats: 30,
      mosqueId: mosque2.id,
    },
  });

  const maktab3 = await prisma.maktab.upsert({
    where: { id: "seed-maktab-003" },
    update: {},
    create: {
      id: "seed-maktab-003",
      name: "Rajshahi Central Maktab",
      teacherName: "Maulana Yusuf",
      teacherPhone: "01912345678",
      totalSeats: 40,
      mosqueId: mosque3.id,
    },
  });

  console.log("Maktabs created ✅");

  // Create students
  await prisma.student.upsert({
    where: { id: "seed-student-001" },
    update: {},
    create: {
      id: "seed-student-001",
      name: "Ahmed Abdullah",
      age: 10,
      address: "Mirpur, Dhaka",
      guardianPhone: "01612345678",
      maktabId: maktab1.id,
    },
  });

  await prisma.student.upsert({
    where: { id: "seed-student-002" },
    update: {},
    create: {
      id: "seed-student-002",
      name: "Omar Faruk",
      age: 12,
      address: "Mohammadpur, Dhaka",
      guardianPhone: "01512345678",
      maktabId: maktab1.id,
    },
  });

  await prisma.student.upsert({
    where: { id: "seed-student-003" },
    update: {},
    create: {
      id: "seed-student-003",
      name: "Yusuf Ali",
      age: 8,
      address: "Old Dhaka",
      guardianPhone: "01412345678",
      maktabId: maktab2.id,
    },
  });

  console.log("Students created ✅");

  // Create fundings
  await prisma.funding.upsert({
    where: { id: "seed-funding-001" },
    update: {},
    create: {
      id: "seed-funding-001",
      donorName: "Anonymous",
      amount: 5000,
      note: "For buying books",
      maktabId: maktab1.id,
    },
  });

  await prisma.funding.upsert({
    where: { id: "seed-funding-002" },
    update: {},
    create: {
      id: "seed-funding-002",
      donorName: "Abdul Rahman",
      amount: 10000,
      note: "For renovation",
      maktabId: maktab1.id,
    },
  });

  await prisma.funding.upsert({
    where: { id: "seed-funding-003" },
    update: {},
    create: {
      id: "seed-funding-003",
      donorName: "Anonymous",
      amount: 3000,
      note: "Monthly donation",
      maktabId: maktab2.id,
    },
  });

  console.log("Fundings created ✅");

  // Create events
  await prisma.event.upsert({
    where: { id: "seed-event-001" },
    update: {},
    create: {
      id: "seed-event-001",
      title: "Quran Mahfil",
      topic: "The Importance of Quran",
      speaker: "Maulana Abdullah",
      eventDate: new Date("2026-07-15"),
      eventTime: "08:00 PM",
      mosqueId: mosque1.id,
    },
  });

  await prisma.event.upsert({
    where: { id: "seed-event-002" },
    update: {},
    create: {
      id: "seed-event-002",
      title: "Hadith Conference",
      topic: "Following the Sunnah of Prophet",
      speaker: "Dr. Muhammad Saifullah",
      eventDate: new Date("2026-08-01"),
      eventTime: "10:00 AM",
      mosqueId: mosque2.id,
    },
  });

  await prisma.event.upsert({
    where: { id: "seed-event-003" },
    update: {},
    create: {
      id: "seed-event-003",
      title: "Islamic Finance Seminar",
      topic: "Halal Banking and Investment",
      speaker: "Professor Abdul Aziz",
      eventDate: new Date("2026-08-20"),
      eventTime: "03:00 PM",
      mosqueId: mosque3.id,
    },
  });

  console.log("Events created ✅");

  // Create questions
  const question1 = await prisma.question.upsert({
    where: { id: "seed-question-001" },
    update: {},
    create: {
      id: "seed-question-001",
      title: "What is the ruling on missing Fajr prayer?",
      body: "I sometimes miss Fajr prayer due to oversleeping. What should I do?",
      category: "Prayer",
      userId: user1.id,
    },
  });

  const question2 = await prisma.question.upsert({
    where: { id: "seed-question-002" },
    update: {},
    create: {
      id: "seed-question-002",
      title: "Is it permissible to pray in congregation at home?",
      body: "Due to illness I cannot go to mosque. Can I pray in congregation at home with my family?",
      category: "Prayer",
      userId: user2.id,
    },
  });

  const question3 = await prisma.question.upsert({
    where: { id: "seed-question-003" },
    update: {},
    create: {
      id: "seed-question-003",
      title: "What is the best time to give Zakat?",
      body: "I want to know when is the best time to give Zakat and how to calculate it.",
      category: "Zakat",
      userId: user1.id,
    },
  });

  console.log("Questions created ✅");

  // Create answers
  await prisma.answer.upsert({
    where: { id: "seed-answer-001" },
    update: {},
    create: {
      id: "seed-answer-001",
      body: "You should make up the missed prayer as soon as you wake up. This is called Qada prayer. Also try to sleep early and set multiple alarms.",
      isAccepted: true,
      userId: admin.id,
      questionId: question1.id,
    },
  });

  await prisma.answer.upsert({
    where: { id: "seed-answer-002" },
    update: {},
    create: {
      id: "seed-answer-002",
      body: "Yes it is permissible and highly encouraged to pray in congregation at home with your family when you cannot attend the mosque.",
      isAccepted: true,
      userId: admin.id,
      questionId: question2.id,
    },
  });

  await prisma.answer.upsert({
    where: { id: "seed-answer-003" },
    update: {},
    create: {
      id: "seed-answer-003",
      body: "Zakat should be given after one lunar year has passed on your wealth. The nisab is 85 grams of gold or 595 grams of silver. The rate is 2.5% of your total savings.",
      isAccepted: false,
      userId: user2.id,
      questionId: question3.id,
    },
  });

  console.log("Answers created ✅");
  console.log("🎉 Seeding complete!");
}

main()
  .catch((e) => {
    console.error(e);
    process.exit(1);
  })
  .finally(async () => {
    await prisma.$disconnect();
  });
