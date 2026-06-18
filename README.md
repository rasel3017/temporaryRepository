// Add a new Maktab
export const addMaktab = async (req, res) => {
  try {
    const { name, teacherName, teacherPhone, totalSeats, mosqueId } = req.body;

    const mosque = await prisma.mosque.findUnique({
      where: { id: mosqueId },
    });

    if (!mosque) {
      return res.status(404).json({
        success: false,
        message: "Mosque not found",
      });
    }

    const maktab = await prisma.maktab.create({
      data: { name, teacherName, teacherPhone, totalSeats, mosqueId },
    });

    res.status(201).json({
      success: true,
      message: "Maktab added successfully",
      data: maktab,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Get Maktabs by Mosque
export const getMaktabsByMosque = async (req, res) => {
  try {
    const { mosqueId } = req.params;

    const maktabs = await prisma.maktab.findMany({
      where: { mosqueId },
    });

    res.status(200).json({
      success: true,
      count: maktabs.length,
      data: maktabs,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Enroll a student
export const enrollStudent = async (req, res) => {
  try {
    const { maktabId } = req.params;
    const { name, age, address, guardianPhone } = req.body;

    const maktab = await prisma.maktab.findUnique({
      where: { id: maktabId },
      include: { students: true },
    });

    if (!maktab) {
      return res.status(404).json({
        success: false,
        message: "Maktab not found",
      });
    }

    if (maktab.students.length >= maktab.totalSeats) {
      return res.status(400).json({
        success: false,
        message: "Maktab is full, no seats available",
      });
    }

    const student = await prisma.student.create({
      data: { name, age, address, guardianPhone, maktabId },
    });

    res.status(201).json({
      success: true,
      message: "Student enrolled successfully",
      data: student,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Get students by Maktab
export const getStudentsByMaktab = async (req, res) => {
  try {
    const { maktabId } = req.params;

    const students = await prisma.student.findMany({
      where: { maktabId },
    });

    res.status(200).json({
      success: true,
      count: students.length,
      data: students,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Add funding
export const addFunding = async (req, res) => {
  try {
    const { maktabId } = req.params;
    console.log("Full body:", req.body);
    const { note, amount } = req.body;
    console.log(req.body);
    console.log(req.body.amount);
    console.log(req.body["amount"]);
    console.log(Object.keys(req.body));
    console.log("amount:",amount,"type:",typeof amount)
    const donorName = req.body.donorName || "Anonymous";

    const maktab = await prisma.maktab.findUnique({
      where: { id: maktabId },
    });

    if (!maktab) {
      return res.status(404).json({
        success: false,
        message: "Maktab not found",
      });
    }

    const funding = await prisma.funding.create({
      data: { donorName, amount: Number(amount), note, maktabId },
    });

    res.status(201).json({
      success: true,
      message: "Funding added successfully",
      data: funding,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};


//terminal
Restarting 'src/server.js'
DB Connected via Prisma
Server is running on port 3000
Full body: { ammount: 5000, note: 'For bying books' }
{ ammount: 5000, note: 'For bying books' }
undefined
undefined
[ 'ammount', 'note' ]
amount: undefined type: undefined
prisma:query SELECT "public"."Maktab"."id", "public"."Maktab"."name", "public"."Maktab"."teacherName", "public"."Maktab"."teacherPhone", "public"."Maktab"."totalSeats", "public"."Maktab"."mosqueId" FROM "public"."Maktab" WHERE ("public"."Maktab"."id" = $1 AND 1=1) LIMIT $2 OFFSET $3
prisma:query INSERT INTO "public"."Funding" ("id","donorName","amount","note","donatedAt","maktabId") VALUES ($1,$2,$3,$4,$5,$6) RETURNING "public"."Funding"."id", "public"."Funding"."donorName", "public"."Funding"."amount", "public"."Funding"."note", "public"."Funding"."donatedAt", "public"."Funding"."maktabId"
