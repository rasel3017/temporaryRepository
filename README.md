import express from "express";
import {
  addMosque,
  getMosquesByRegion,
  getMosqueDetails,
  searchMosque,
} from "../controllers/mosque.controller.js";

const router = express.Router();

router.post("/", addMosque);
router.get("/region/:region", getMosquesByRegion);
router.get("/:id", getMosqueDetails);
router.get("/search/:name", searchMosque);

export default router;
