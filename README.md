import express from "express";
import {
  createEvent,
  getEventsByRegion,
  getEventDetails,
  deleteEvent,
} from "../controllers/event.controller.js";
import { protect, adminOnly } from "../middleware/auth.middleware.js";

const router = express.Router();

router.post("/", protect, adminOnly, createEvent);
router.get("/region/:region", getEventsByRegion);
router.get("/:id", getEventDetails);
router.delete("/:id", protect, adminOnly, deleteEvent);

export default router;
