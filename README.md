// Create event
export const createEvent = async (req, res) => {
  try {
    const { title, topic, speaker, eventDate, eventTime, location, description, imageUrl, isFree, mosqueId } = req.body;

    const mosque = await prisma.mosque.findUnique({
      where: { id: mosqueId },
    });

    if (!mosque) {
      return res.status(404).json({
        success: false,
        message: "Mosque not found",
      });
    }

    const event = await prisma.event.create({
      data: {
        title,
        topic,
        speaker,
        eventDate: new Date(eventDate),
        eventTime,
        location,
        description,
        imageUrl,
        isFree: isFree !== undefined ? isFree : true,
        mosqueId,
      },
    });

    res.status(201).json({
      success: true,
      message: "Event created successfully",
      data: event,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};
