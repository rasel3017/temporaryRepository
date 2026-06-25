// Add a new Maktab
export const addMaktab = async (req, res) => {
  try {
    const { name, address, teacherName, teacherPhone, totalSeats, coursesOffered, imageUrl, mosqueId } = req.body;

    if (mosqueId) {
      const mosque = await prisma.mosque.findUnique({
        where: { id: mosqueId },
      });

      if (!mosque) {
        return res.status(404).json({
          success: false,
          message: "Mosque not found",
        });
      }
    }

    const maktab = await prisma.maktab.create({
      data: {
        name,
        address,
        teacherName,
        teacherPhone,
        totalSeats,
        coursesOffered,
        imageUrl,
        mosqueId,
      },
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
