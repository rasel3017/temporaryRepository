export const validateCreateEvent = (req, res, next) => {
  const title = req.body?.title;
  const topic = req.body?.topic;
  const speaker = req.body?.speaker;
  const eventDate = req.body?.eventDate;
  const eventTime = req.body?.eventTime;
  const mosqueId = req.body?.mosqueId;

  if (!title || !topic || !speaker || !eventDate || !eventTime || !mosqueId) {
    return res.status(400).json({
      success: false,
      message: "Title, topic, speaker, eventDate, eventTime and mosqueId are required",
    });
  }

  next();
};
