# Attendify-Hub
**Attendify Hub** is a web-based attendance management system developed using **React.js** and **Node.js**. It enables organizations and educational institutions to efficiently track, manage, and monitor attendance records through a user-friendly interface. The system provides secure user authentication, real-time attendance,central data management


const express = require("express");
const cors = require("cors");

const app = express();
const PORT = process.env.PORT || 5000;

app.use(cors());
app.use(express.json());



// Sample attendance data

let attendance = [
  {
    id: 1,
    name: "John Doe",
    date: "2026-06-02",
    status: "Present"
  }
];



// Home Route

app.get("/", (req, res) => {
  res.json({
    message: "Welcome to Attendify Hub API"
  });
});



// Get all attendance records

app.get("/api/attendance", (req, res) => {
  res.json(attendance);
});




// Add attendance record

app.post("/api/attendance", (req, res) => {
  const record = {
    id: attendance.length + 1,
    ...req.body
  };

  attendance.push(record);
  res.status(201).json({
    message: "Attendance recorded successfully",
    record
  });
});



// Update attendance

app.put("/api/attendance/:id", (req, res) => {
  const id = parseInt(req.params.id);

  attendance = attendance.map(record =>
    record.id === id ? { ...record, ...req.body } : record
  );

  res.json({
    message: "Attendance updated successfully"
  });
});



// Delete attendance record

app.delete("/api/attendance/:id", (req, res) => {
  const id = parseInt(req.params.id);

  attendance = attendance.filter(record => record.id !== id);

  res.json({
    message: "Attendance deleted successfully"
  });
});

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
