import { prisma } from "../config/db.js";

// Post a question
export const postQuestion = async (req, res) => {
  try {
    const { title, body, category } = req.body;
    const userId = req.user.userId;

    const question = await prisma.question.create({
      data: { title, body, category, userId },
    });

    res.status(201).json({
      success: true,
      message: "Question posted successfully",
      data: question,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Post an answer
export const postAnswer = async (req, res) => {
  try {
    const { questionId } = req.params;
    const { body } = req.body;
    const userId = req.user.userId;

    const question = await prisma.question.findUnique({
      where: { id: questionId },
    });

    if (!question) {
      return res.status(404).json({
        success: false,
        message: "Question not found",
      });
    }

    const answer = await prisma.answer.create({
      data: { body, userId, questionId },
    });

    res.status(201).json({
      success: true,
      message: "Answer posted successfully",
      data: answer,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Get all questions
export const getAllQuestions = async (req, res) => {
  try {
    const questions = await prisma.question.findMany({
      include: {
        user: { select: { name: true } },
        answers: true,
      },
      orderBy: { createdAt: "desc" },
    });

    res.status(200).json({
      success: true,
      count: questions.length,
      data: questions,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Get answers by question
export const getAnswersByQuestion = async (req, res) => {
  try {
    const { questionId } = req.params;

    const answers = await prisma.answer.findMany({
      where: { questionId },
      include: {
        user: { select: { name: true } },
      },
      orderBy: { createdAt: "asc" },
    });

    res.status(200).json({
      success: true,
      count: answers.length,
      data: answers,
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};

// Delete a question 
export const deleteQuestion = async (req, res) => {
  try {
    const { questionId } = req.params;

    const question = await prisma.question.findUnique({
      where: { id: questionId },
    });

    if (!question) {
      return res.status(404).json({
        success: false,
        message: "Question not found",
      });
    }

    await prisma.answer.deleteMany({
      where: { questionId },
    });

    await prisma.question.delete({
      where: { id: questionId },
    });

    res.status(200).json({
      success: true,
      message: "Question and its answers deleted successfully",
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message,
    });
  }
};
