export const validateAddMosque = (req, res, next) => {
  const { name, address, region } = req.body;

  if (!name || !address || !region) {
    return res.status(400).json({
      success: false,
      message: "Name, address and region are required",
    });
  }

  if (name.trim().length < 3) {
    return res.status(400).json({
      success: false,
      message: "Mosque name must be at least 3 characters",
    });
  }

  next();
};
