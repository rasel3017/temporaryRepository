import { prisma } from "../config/db.js";

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
    const { donorName, amount, note } = req.body;

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
      data: { donorName, amount, note, maktabId },
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

// Get funding history
export const getFundingHistory = async (req, res) => {
  try {
    const { maktabId } = req.params;

    const fundings = await prisma.funding.findMany({
      where: { maktabId },
      orderBy: { donatedAt: "desc" },
    });

    const total = fundings.reduce((sum, f) => sum + f.amount, 0);

    res.status(200).json({
      success: true,
      count: fundings.length,
      totalAmount: total,
      data: fundings,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};
