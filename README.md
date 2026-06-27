await prisma.event.upsert({
  where: { id: "seed-event-001" },
  update: {},
  create: {
    id: "seed-event-001",
    title: "Quran Mahfil 2026",
    topic: "The Importance of Quran in Daily Life",
    speaker: "Maulana Abdullah Al Faruki",
    eventDate: new Date("2026-07-15"),
    eventTime: "08:00 PM",
    location: "Baitul Mukarram Mosque, Dhaka",
    description: "Join us for a beautiful Mahfil. Free Quran will be distributed. Biryani will be served after the event.",
    imageUrl: "images/event1.jpg",
    isFree: true,
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
    location: "Star Mosque, Old Dhaka",
    description: "A grand conference on Hadith sciences. Certificate will be given to participants.",
    imageUrl: "images/event2.jpg",
    isFree: true,
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
    location: "Rajshahi City Hall",
    description: "Learn about halal investment and banking. Entry fee: 200 BDT.",
    imageUrl: "images/event3.jpg",
    isFree: false,
    mosqueId: mosque3.id,
  },
});

await prisma.event.upsert({
  where: { id: "seed-event-004" },
  update: {},
  create: {
    id: "seed-event-004",
    title: "Independent Quran Mahfil",
    topic: "Love for Quran",
    speaker: "Maulana Tariq Jameel",
    eventDate: new Date("2026-07-20"),
    eventTime: "07:00 PM",
    location: "Dhaka City College Ground",
    description: "Open for all. Free entry. Biryani will be served after the Mahfil.",
    imageUrl: "images/event4.jpg",
    isFree: true,
    mosqueId: null,
  },
});
