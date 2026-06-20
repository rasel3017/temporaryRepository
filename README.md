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

  console.log("Admin created:", admin.email);

  // Create mosque
  const mosque = await prisma.mosque.upsert({
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

  console.log("Mosque created:", mosque.name);

  // Create maktab
  const maktab = await prisma.maktab.upsert({
    where: { id: "seed-maktab-001" },
    update: {},
    create: {
      id: "seed-maktab-001",
      name: "Baitul Mukarram Maktab",
      teacherName: "Maulana Abdul Karim",
      teacherPhone: "01712345678",
      totalSeats: 50,
      mosqueId: mosque.id,
    },
  });

  console.log("Maktab created:", maktab.name);

  // Create event
  const event = await prisma.event.upsert({
    where: { id: "seed-event-001" },
    update: {},
    create: {
      id: "seed-event-001",
      title: "Quran Mahfil",
      topic: "The Importance of Quran",
      speaker: "Maulana Abdullah",
      eventDate: new Date("2026-07-15"),
      eventTime: "08:00 PM",
      mosqueId: mosque.id,
    },
  });

  console.log("Event created:", event.title);

  // Create question
  const question = await prisma.question.upsert({
    where: { id: "seed-question-001" },
    update: {},
    create: {
      id: "seed-question-001",
      title: "What is the ruling on missing Fajr prayer?",
      body: "I sometimes miss Fajr prayer due to oversleeping. What should I do?",
      category: "Prayer",
      userId: admin.id,
    },
  });

  console.log("Question created:", question.title);

  console.log("Seeding complete!");
}

main()
  .catch((e) => {
    console.error(e);
    process.exit(1);
  })
  .finally(async () => {
    await prisma.$disconnect();
  });
