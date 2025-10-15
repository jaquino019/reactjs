/* Reset styles */
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

html, body {
    height: 100%;
    font-family: Arial, sans-serif;
}

body {
    display: flex;
    flex-direction: column;
}

/* Container for the content */
.container {
    flex: 1;
    padding: 20px;
}

/* Header styling */
header {
    background-color: #333;
    color: white;
    padding: 20px;
    text-align: center;
}

nav a {
    color: white;
    margin: 0 10px;
    text-decoration: none;
}

/* Footer fixed to bottom */
footer {
    background-color: #333;
    color: white;
    text-align: center;
    padding: 10px;
}

/* Grid layout for skills (5x5) */
.skill-container {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 20px;
    margin-top: 20px;
}

.skill {
    text-align: center;
}

.skill img {
    width: 60px;
    height: 60px;
}

/* Responsive fallback (optional) */
@media (max-width: 768px) {
    .skill-container {
        grid-template-columns: repeat(2, 1fr);
    }
}
