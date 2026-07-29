export const getAllEvents = async (req, res) => {
  try {
    const events = await prisma.event.findMany({
      orderBy: { eventDate: "asc" },
      include: {
        mosque: { select: { name: true, region: true } }
      }
    });

    res.status(200).json({
      success: true,
      count: events.length,
      data: events,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};
