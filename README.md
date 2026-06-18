import express from "express";
import {
  addMaktab,
  getMaktabsByMosque,
  enrollStudent,
  getStudentsByMaktab,
  addFunding,
  getFundingHistory,
} from "../controllers/maktab.controller.js";
import { protect, adminOnly } from "../middleware/auth.middleware.js";

const router = express.Router();

router.post("/", protect, adminOnly, addMaktab);
router.get("/mosque/:mosqueId", getMaktabsByMosque);
router.post("/:maktabId/students", protect, enrollStudent);
router.get("/:maktabId/students", getStudentsByMaktab);
router.post("/:maktabId/funding", protect, adminOnly, addFunding);
router.get("/:maktabId/funding", getFundingHistory);

export default router;
