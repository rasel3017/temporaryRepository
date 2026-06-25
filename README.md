export const createEvent = async (req, res) => {
  try {
    const { title, topic, speaker, eventDate, eventTime, location, description, imageUrl, isFree, mosqueId, maktabId } = req.body;

    if (mosqueId) {
      const mosque = await prisma.mosque.findUnique({ where: { id: mosqueId } });
      if (!mosque) {
        return res.status(404).json({ success: false, message: "Mosque not found" });
      }
    }

    if (maktabId) {
      const maktab = await prisma.maktab.findUnique({ where: { id: maktabId } });
      if (!maktab) {
        return res.status(404).json({ success: false, message: "Maktab not found" });
      }
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
        maktabId,
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
