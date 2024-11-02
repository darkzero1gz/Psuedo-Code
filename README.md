# Psuedo-Code
//Psuedo code นี้คือการเขียนขั้นตอนของโปรแกรมโดยประกาศตัวแปร ฟังก์ชันสำหรับแสดงเมนู รับค่า ตรวจคำตอบ อัปเดตคะแนน และแสดงอันดับสูงสุด เพื่อให้เห็นลำดับขั้นการทำงานของโปรแกรมอย่างชัดเจน





CONSTANT MAX_SCORES = 10
DECLARE players[MAX_SCORES] AS STRING ARRAY
DECLARE highScores[MAX_SCORES] AS INTEGER ARRAY, INITIALIZED TO 0
DECLARE times[MAX_SCORES] AS DOUBLE ARRAY, INITIALIZED TO 0
DECLARE modes[MAX_SCORES] AS STRING ARRAY
DECLARE totalScores AS INTEGER, INITIALIZED TO 0

FUNCTION displayMenu
    PRINT "--- English Tense Game ---"
    PRINT "1. Present Simple"
    PRINT "2. Past Simple"
    PRINT "3. Future Simple"
    PRINT "4. Show score board"
    PRINT "5. Exit"
END FUNCTION

FUNCTION getModeName(choice AS INTEGER) RETURNS STRING
    IF choice == 1 THEN RETURN "Present Simple"
    ELSE IF choice == 2 THEN RETURN "Past Simple"
    ELSE IF choice == 3 THEN RETURN "Future Simple"
    RETURN ""
END FUNCTION

FUNCTION playGame(choice AS INTEGER) RETURNS INTEGER
    SET score = 0
    IF choice == 1 THEN
        // Conduct questions for Present Simple tense
        FOR EACH QUESTION in PresentSimpleQuestions DO
            PROMPT user FOR answer
            IF answer IS correct THEN INCREMENT score
            ELSE PRINT correct answer
        END FOR
    ELSE IF choice == 2 THEN
        // Conduct questions for Past Simple tense
        FOR EACH QUESTION in PastSimpleQuestions DO
            PROMPT user FOR answer
            IF answer IS correct THEN INCREMENT score
            ELSE PRINT correct answer
        END FOR
    ELSE IF choice == 3 THEN
        // Conduct questions for Future Simple tense
        FOR EACH QUESTION in FutureSimpleQuestions DO
            PROMPT user FOR answer
            IF answer IS correct THEN INCREMENT score
            ELSE PRINT correct answer
        END FOR
    END IF
    RETURN score
END FUNCTION

FUNCTION updateHighScores(playerName AS STRING, score AS INTEGER, timeTaken AS DOUBLE, mode AS STRING)
    IF totalScores < MAX_SCORES THEN
        STORE playerName, score, timeTaken, and mode IN respective arrays at index totalScores
        INCREMENT totalScores
    ELSE
        // Find and replace lowest score or slowest time if current score is better or faster
        FIND index of lowest score or highest time
        IF current score > lowest score OR (current score == lowest score AND current time is faster)
            REPLACE values at lowest score index with playerName, score, timeTaken, mode
    END IF
END FUNCTION

FUNCTION sortScores
    FOR i FROM 0 TO totalScores - 1 DO
        FOR j FROM 0 TO totalScores - i - 1 DO
            IF highScores[j] < highScores[j + 1] OR (highScores[j] == highScores[j + 1] AND times[j] > times[j + 1]) THEN
                SWAP highScores[j], highScores[j + 1]
                SWAP players[j], players[j + 1]
                SWAP times[j], times[j + 1]
                SWAP modes[j], modes[j + 1]
            END IF
        END FOR
    END FOR
END FUNCTION

FUNCTION displayHighScores
    CALL sortScores
    PRINT "--- High Scores ---"
    FOR i FROM 0 TO totalScores - 1 DO
        PRINT i+1, players[i], modes[i], highScores[i], times[i]
    END FOR
    PRINT "--------------------"
END FUNCTION

FUNCTION isNumber(str AS STRING) RETURNS BOOLEAN
    FOR EACH character c IN str DO
        IF c IS NOT a digit THEN RETURN false
    END FOR
    RETURN true
END FUNCTION

MAIN
    PROMPT user FOR playerName

    WHILE true DO
        CALL displayMenu
        PROMPT user FOR input
        IF input IS a number THEN
            SET choice TO integer value of input
            IF choice IS 1, 2, or 3 THEN
                CALL playGame WITH choice AND RECEIVE score
                RECORD time taken for game
                CALL getModeName WITH choice AND RECEIVE modeName
                CALL updateHighScores WITH playerName, score, time taken, modeName
            ELSE IF choice IS 4 THEN
                CALL displayHighScores
            ELSE IF choice IS 5 THEN
                EXIT
            ELSE
                PRINT "Invalid choice"
        ELSE
            PRINT "Please enter a valid number."
    END WHILE
END MAIN
