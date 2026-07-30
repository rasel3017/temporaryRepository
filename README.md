
router.get("/seed-now", async (req, res) => {
  try {
    const { exec } = await import("child_process");
    exec("node prisma/seed.js", (error, stdout, stderr) => {
      if (error) {
        return res.json({ success: false, message: error.message });
      }
      res.json({ success: true, message: "Seeded!", output: stdout });
    });
  } catch (err) {
    res.json({ success: false, message: err.message });
  }
});
