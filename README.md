export const searchMaktab = async (req, res) => {
  try {
    const { name } = req.params;

    const maktabs = await prisma.maktab.findMany({
      where: {
        name: {
          contains: name,
          mode: "insensitive"
        }
      },
      include: {
        mosque: { select: { name: true, region: true } }
      }
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
