import express from "express";
import {
  postQuestion,
  postAnswer,
  getAllQuestions,
  getAnswersByQuestion,
  deleteQuestion,
} from "../controllers/qa.controller.js";
import { protect, adminOnly } from "../middleware/auth.middleware.js";

const router = express.Router();

router.post("/questions", protect, postQuestion);
router.post("/questions/:questionId/answers", protect, postAnswer);
router.get("/questions", getAllQuestions);
router.get("/questions/:questionId/answers", getAnswersByQuestion);
router.delete("/questions/:questionId", protect, adminOnly, deleteQuestion);

export default router;
