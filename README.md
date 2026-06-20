export const validateAddMaktab = (req, res, next) => {
  const { name, teacherName, teacherPhone, totalSeats, mosqueId } = req.body;

  if (!name || !teacherName || !teacherPhone || !totalSeats || !mosqueId) {
    return res.status(400).json({
      success: false,
      message: "Name, teacherName, teacherPhone, totalSeats and mosqueId are required",
    });
  }

  next();
};

export const validateEnrollStudent = (req, res, next) => {
  const { name, age, guardianPhone } = req.body;

  if (!name || !age || !guardianPhone) {
    return res.status(400).json({
      success: false,
      message: "Name, age and guardianPhone are required",
    });
  }

  if (age < 4 || age > 18) {
    return res.status(400).json({
      success: false,
      message: "Student age must be between 4 and 18",
    });
  }

  next();
};

export const validateAddFunding = (req, res, next) => {
  const { amount } = req.body;

  if (!amount) {
    return res.status(400).json({
      success: false,
      message: "Amount is required",
    });
  }

  if (amount <= 0) {
    return res.status(400).json({
      success: false,
      message: "Amount must be greater than 0",
    });
  }

  next();
};
