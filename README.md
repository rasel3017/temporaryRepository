import { prisma } from "../config/db.js";

// Add a new mosque
const { name, address, region, latitude, longitude, imamName, muazzinName, imageUrl, fajrTime, zuhrTime, asrTime, maghribTime, ishaTime } = req.body;

const mosque = await prisma.mosque.create({
  data: { 
    name, address, region, latitude, longitude,
    imamName, muazzinName, imageUrl,
    fajrTime, zuhrTime, asrTime, maghribTime, ishaTime,
    user: { connect: { id: userId } }
  },
});


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
