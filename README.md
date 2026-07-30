export const getAllMosques = async (req, res) => {
  try {
    const mosques = await prisma.mosque.findMany();
    res.status(200).json({ success: true, count: mosques.length, data: mosques });
  } catch (error) {
    res.status(500).json({ success: false, message: error.message });
  }
};
