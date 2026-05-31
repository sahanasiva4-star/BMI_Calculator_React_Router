# Ex06 BMI Calculator
## Date: 27.05.26

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM
~~~
# main.jsx:
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./App.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
~~~
~~~
# app.jsx:
import { useState } from "react";
import "./App.css";

function App() {
  const [height, setHeight] = useState("");
  const [weight, setWeight] = useState("");
  const [bmi, setBmi] = useState(null);
  const [status, setStatus] = useState("");

  const calculateBMI = () => {
    if (!height || !weight) {
      alert("Please enter height and weight");
      return;
    }

    const heightInMeters = height / 100;
    const bmiValue = (
      weight /
      (heightInMeters * heightInMeters)
    ).toFixed(1);

    setBmi(bmiValue);

    if (bmiValue < 18.5) {
      setStatus("Underweight");
    } else if (bmiValue < 25) {
      setStatus("Normal Weight");
    } else if (bmiValue < 30) {
      setStatus("Overweight");
    } else {
      setStatus("Obese");
    }
  };

  const resetFields = () => {
    setHeight("");
    setWeight("");
    setBmi(null);
    setStatus("");
  };

  return (
    <div className="container">
      <div className="card">
        <h1>BMI Calculator</h1>

        <div className="input-group">
          <label>Height (cm)</label>
          <input
            type="number"
            placeholder="Enter height"
            value={height}
            onChange={(e) => setHeight(e.target.value)}
          />
        </div>

        <div className="input-group">
          <label>Weight (kg)</label>
          <input
            type="number"
            placeholder="Enter weight"
            value={weight}
            onChange={(e) => setWeight(e.target.value)}
          />
        </div>

        <div className="buttons">
          <button onClick={calculateBMI}>
            Calculate BMI
          </button>

          <button className="reset" onClick={resetFields}>
            Reset
          </button>
        </div>

        {bmi && (
          <div className="result">
            <h2>Your BMI: {bmi}</h2>
            <p>Status: {status}</p>
          </div>
        )}
      </div>
    </div>
  );
}

export default App;
~~~
~~~
# app.css:
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

body {
  min-height: 100vh;
  background: linear-gradient(
    135deg,
    #4f46e5,
    #7c3aed,
    #9333ea
  );
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
}

.card {
  width: 400px;
  max-width: 100%;
  background: white;
  padding: 30px;
  border-radius: 20px;
  box-shadow: 0 8px 25px rgba(0,0,0,0.2);
}

.card h1 {
  text-align: center;
  margin-bottom: 25px;
  color: #4f46e5;
}

.input-group {
  margin-bottom: 18px;
}

.input-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: 600;
}

.input-group input {
  width: 100%;
  padding: 12px;
  border: 2px solid #ddd;
  border-radius: 10px;
  font-size: 16px;
}

.input-group input:focus {
  outline: none;
  border-color: #4f46e5;
}

.buttons {
  display: flex;
  gap: 10px;
}

button {
  flex: 1;
  padding: 12px;
  border: none;
  cursor: pointer;
  border-radius: 10px;
  font-size: 16px;
  color: white;
  background: #4f46e5;
  transition: 0.3s;
}

button:hover {
  transform: translateY(-2px);
}

.reset {
  background: #ef4444;
}

.result {
  margin-top: 25px;
  text-align: center;
  padding: 20px;
  border-radius: 12px;
  background: #f3f4f6;
}

.result h2 {
  color: #4f46e5;
  margin-bottom: 10px;
}

.result p {
  font-size: 18px;
  font-weight: 600;
}

@media (max-width: 500px) {
  .buttons {
    flex-direction: column;
  }

  .card {
    padding: 20px;
  }
}
~~~


## OUTPUT
<img width="1919" height="926" alt="image" src="https://github.com/user-attachments/assets/1523a5d3-6696-4a68-b354-41e3ab90c237" />


## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
