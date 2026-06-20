export const validatePostQuestion = (req, res, next) => {
  const title = req.body?.title;
  const body = req.body?.body;
  const category = req.body?.category;

  if (!title || !body || !category) {
    return res.status(400).json({
      success: false,
      message: "Title, body and category are required",
    });
  }

  next();
};

export const validatePostAnswer = (req, res, next) => {
  const body = req.body?.body;

  if (!body) {
    return res.status(400).json({
      success: false,
      message: "Answer body is required",
    });
  }

  next();
};
