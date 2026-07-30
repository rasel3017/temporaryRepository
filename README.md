// Temporary seed route
app.get("/seed-now", async (req, res) => {
  const { exec } = await import("child_process");
  exec("node prisma/seed.js", (error, stdout) => {
    if (error) return res.json({ success: false, message: error.message });
    res.json({ success: true, message: "Seeded!", output: stdout });
  });
});
