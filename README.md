import { prisma } from "../config/db.js";

// Add a new mosque
export const addMosque = async (req, res) => {
  try {
    const { name, address, region, latitude, longitude } = req.body;

    const mosque = await prisma.mosque.create({
      data: { name, address, region, latitude, longitude },
    });

    res.status(201).json({
      success: true,
      message: "Mosque added successfully",
      data: mosque,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Get mosques by region
export const getMosquesByRegion = async (req, res) => {
  try {
    const { region } = req.params;

    const mosques = await prisma.mosque.findMany({
      where: { region },
    });

    res.status(200).json({
      success: true,
      count: mosques.length,
      data: mosques,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Get mosque details
export const getMosqueDetails = async (req, res) => {
  try {
    const { id } = req.params;

    const mosque = await prisma.mosque.findUnique({
      where: { id },
      include: {
        maktabs: true,
        events: true,
      },
    });

    if (!mosque) {
      return res.status(404).json({
        success: false,
        message: "Mosque not found",
      });
    }

    res.status(200).json({
      success: true,
      data: mosque,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Search mosque by name
export const searchMosque = async (req, res) => {
  try {
    const { name } = req.params;

    const mosques = await prisma.mosque.findMany({
      where: {
        name: {
          contains: name,
          mode: "insensitive",
        },
      },
    });

    res.status(200).json({
      success: true,
      count: mosques.length,
      data: mosques,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};
