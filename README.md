export const validateAddMaktab = (req, res, next) => {
  const name = req.body?.name;
  const teacherName = req.body?.teacherName;
  const teacherPhone = req.body?.teacherPhone;
  const totalSeats = req.body?.totalSeats;
  const mosqueId = req.body?.mosqueId;

  if (!name || !teacherName || !teacherPhone || !totalSeats || !mosqueId) {
    return res.status(400).json({
      success: false,
      message: "Name, teacherName, teacherPhone, totalSeats and mosqueId are required",
    });
  }

  next();
};

export const validateEnrollStudent = (req, res, next) => {
  const name = req.body?.name;
  const age = req.body?.age;
  const guardianPhone = req.body?.guardianPhone;

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
  const amount = req.body?.amount;

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
