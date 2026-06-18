// Delete mosque
export const deleteMosque = async (req, res) => {
  try {
    const { id } = req.params;

    const mosque = await prisma.mosque.findUnique({
      where: { id },
    });

    if (!mosque) {
      return res.status(404).json({
        success: false,
        message: "Mosque not found",
      });
    }

    await prisma.mosque.delete({
      where: { id },
    });

    res.status(200).json({
      success: true,
      message: "Mosque deleted successfully",
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};
