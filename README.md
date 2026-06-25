// Add funding to mosque
export const addMosqueFunding = async (req, res) => {
  try {
    const { mosqueId } = req.params;
    const { note } = req.body;
    const amount = Number(req.body.amount);
    const donorName = req.body.donorName || "Anonymous";

    const mosque = await prisma.mosque.findUnique({
      where: { id: mosqueId },
    });

    if (!mosque) {
      return res.status(404).json({
        success: false,
        message: "Mosque not found",
      });
    }

    const funding = await prisma.funding.create({
      data: { donorName, amount, note, mosqueId },
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

// Get mosque funding history
export const getMosqueFundingHistory = async (req, res) => {
  try {
    const { mosqueId } = req.params;

    const fundings = await prisma.funding.findMany({
      where: { mosqueId },
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
