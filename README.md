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

    // Delete all answers first
    await prisma.answer.deleteMany({
      where: { questionId },
    });

    // Then delete the question
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
