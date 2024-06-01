# student-grade-tracker
Contribute to open Source Project for junior students to input and calculate their grades. Java can handle the grading logic, and the front end can be designed with HTML, CSS, and simple JavaScript to get the user input
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grade Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 400px;
            text-align: center;
        }

        form {
            display: flex;
            flex-direction: column;
        }

        label {
            margin-bottom: 8px;
        }

        input {
            padding: 8px;
            margin-bottom: 16px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 16px;
        }

        button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }

        button:hover {
            background-color: #0056b3;
        }

        #result {
            margin-top: 20px;
            font-size: 18px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Grade Calculator</h1>
        <form id="gradeForm">
            <label for="mathGrade">Math Grade:</label>
            <input type="number" id="mathGrade" name="mathGrade" required>
            
            <label for="scienceGrade">Science Grade:</label>
            <input type="number" id="scienceGrade" name="scienceGrade" required>
            
            <label for="englishGrade">En
#the java part
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.node.ObjectNode;

import static spark.Spark.*;

public class GradeCalculator {
    public static void main(String[] args) {
        port(8080);

        post("/calculateGrades", (req, res) -> {
            res.type("application/json");

            ObjectMapper mapper = new ObjectMapper();
            ObjectNode result = mapper.createObjectNode();

            try {
                // Parse JSON request body
                double mathGrade = Double.parseDouble(req.queryParams("mathGrade"));
                double scienceGrade = Double.parseDouble(req.queryParams("scienceGrade"));
                double englishGrade = Double.parseDouble(req.queryParams("englishGrade"));

                // Calculate average grade
                double averageGrade = (mathGrade + scienceGrade + englishGrade) / 3.0;

                // Prepare response
                result.put("averageGrade", averageGrade);

                res.status(200);
            } catch (NumberFormatException e) {
                result.put("error", "Invalid input. Please provide numeric grades.");
                res.status(400);
            }

            return result;
        });
    }
}
