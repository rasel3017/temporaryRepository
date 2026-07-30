export const deleteMaktab = async (req, res) => {
  try {
    const { maktabId } = req.params;

    const maktab = await prisma.maktab.findUnique({
      where: { id: maktabId },
    });

    if (!maktab) {
      return res.status(404).json({
        success: false,
        message: "Maktab not found",
      });
    }

    await prisma.student.deleteMany({ where: { maktabId } });
    await prisma.funding.deleteMany({ where: { maktabId } });
    await prisma.maktab.delete({ where: { id: maktabId } });

    res.status(200).json({
      success: true,
      message: "Maktab deleted successfully",
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};
