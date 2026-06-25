import { prisma } from "../config/db.js";

// Add a new mosque
export const addMosque = async (req, res) => {
  try {
    const { name, address, region, latitude, longitude, imamName, muazzinName, imageUrl, fajrTime, zuhrTime, asrTime, maghribTime, ishaTime } = req.body;
    const userId = req.user.userId;

    const mosque = await prisma.mosque.create({
      data: { 
        name, address, region, latitude, longitude,
        imamName, muazzinName, imageUrl,
        fajrTime, zuhrTime, asrTime, maghribTime, ishaTime,
        user: { connect: { id: userId } }
      },
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
