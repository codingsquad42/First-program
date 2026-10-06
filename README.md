# First-program
// --- 1. GAME VARIABLES ---
var ballX = 200;      // Starting horizontal position of the ball
var ballY = 0;        // Starting height of the ball (top of screen)
var ballSpeed = 4;    // How fast the ball falls down
var basketXX = 160;    // Starting horizontal position of your basket
var score = 0;        // Initial game score

// --- 2. THE MAIN LOOP (Runs 60 times every second) ---
draw = function() {
    // Clear the screen with a light blue sky color
    background(173, 216, 230);
    
    // --- 3. DRAW GAME OBJECTS ---
    // Draw the falling ball (Red Circle)
    fill(255, 0, 0);
    ellipse(ballX, ballY, 20, 20);
    
    // Draw the player basket (Brown Rectangle)
    fill(139, 69, 19);
    rect(basketXX, 360, 80, 20);
    
    // Display the Score text in black font
    fill(0, 0, 0);
    textSize(20);
    text("Score: " + score, 20, 30);
    
    // --- 4. GAME MECHANICS & PHYSICS ---
    // Make the ball fall down automatically
    ballY += ballSpeed;
    
    // Check for keyboard presses to move the basket left/right
    if (keyIsPressed && keyCode === LEFT) {
        basketXX -= 5;
    }
    if (keyIsPressed && keyCode === RIGHT) {
        basketXX += 5;
    }
    
    // --- 5. COLLISION DETECTION (Catching the ball) ---
    // Check if the ball passes the basket height
    if (ballY >= 360 && ballY <= 380) {
        // Check if the ball is horizontally aligned with the basket
        if (ballX >= basketXX && ballX <= basketXX + 80) {
            score += 1;          // Increase score by 1
            ballY = 0;           // Reset ball back to the top
            ballX = random(20, 380); // Move ball to a random column
        }
    }
    
    // --- 6. GAME OVER CHECK ---
    // If the ball falls past the bottom window edge without being caught
    if (ballY > 400) {
        ballY = 0;               // Reset ball back to the top
        ballX = random(20, 380); // Move ball to a random column
        score = 0;               // Reset score back to zero
    }
