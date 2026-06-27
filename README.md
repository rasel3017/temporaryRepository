const maktab1 = await prisma.maktab.upsert({
  where: { id: "seed-maktab-001" },
  update: {},
  create: {
    id: "seed-maktab-001",
    name: "Baitul Mukarram Maktab",
    address: "Topkhana Road, Dhaka",
    teacherName: "Maulana Abdul Karim",
    teacherPhone: "01712345678",
    totalSeats: 50,
    coursesOffered: "Quran Recitation, Tajweed, Islamic Studies, Arabic Language",
    imageUrl: "images/quran1.jpg",
    mosqueId: mosque1.id,
  },
});

const maktab2 = await prisma.maktab.upsert({
  where: { id: "seed-maktab-002" },
  update: {},
  create: {
    id: "seed-maktab-002",
    name: "Star Mosque Maktab",
    address: "Armanitola, Old Dhaka",
    teacherName: "Maulana Ibrahim",
    teacherPhone: "01812345678",
    totalSeats: 30,
    coursesOffered: "Quran Memorization, Hadith, Fiqh",
    imageUrl: "images/quran2.jpg",
    mosqueId: mosque2.id,
  },
});

const maktab3 = await prisma.maktab.upsert({
  where: { id: "seed-maktab-003" },
  update: {},
  create: {
    id: "seed-maktab-003",
    name: "Rajshahi Central Maktab",
    address: "Rajshahi City Center",
    teacherName: "Maulana Yusuf",
    teacherPhone: "01912345678",
    totalSeats: 40,
    coursesOffered: "Quran Recitation, Arabic Language, Islamic History",
    imageUrl: "images/quran3.jpg",
    mosqueId: mosque3.id,
  },
});

const maktab4 = await prisma.maktab.upsert({
  where: { id: "seed-maktab-004" },
  update: {},
  create: {
    id: "seed-maktab-004",
    name: "Independent Darul Quran",
    address: "Mirpur, Dhaka",
    teacherName: "Hafez Muhammad Anas",
    teacherPhone: "01612345678",
    totalSeats: 60,
    coursesOffered: "Hifz Program, Quran Recitation, Tajweed",
    imageUrl: "images/quran4.jpg",
    mosqueId: null,
  },
});
