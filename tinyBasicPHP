<?php

$input = "";

       if ($_SERVER['REQUEST_METHOD'] === 'POST') {

                $input = $_POST['inputValue'];

                $input = "z " . $input;

                }

class TinyBasicInterpreter {

    private $program = array();

    private $variables = array();

    private $input;

    private $forStack = array();

    private $gosubStack = array();

    private $gotoStack = array();

    

    

public function __construct() {

        $this->variables = [];

    }

    

    public function run($code) {

        $this->parseProgram($code);

        $this->executeProgram();

    }

    

    private function parseProgram($code) {

    $lines = explode(";", $code);

    foreach ($lines as $line) {

        $line = trim($line);

        if (!empty($line)) {

            $matches = array();

            preg_match('/^(\d+)\s+(.*)$/', $line, $matches);

            if (count($matches) === 3) {

                $lineNumber = intval($matches[1]);

                $statements = explode(";", $matches[2]);

                foreach ($statements as $statement) {

                    $this->program[$lineNumber] = trim($statement);

                    $lineNumber++;

                }

            }

        }

    }

}

    private function executeProgram() {

        $lineNumber = min(array_keys($this->program));

        while ($lineNumber !== false) {

            $statement = $this->program[$lineNumber];

            $this->executeStatement($statement);

if ($command === "GOTO") {

    return;

}

if ($command === "THEN") {

    return;

}

            $lineNumber = $this->getNextLineNumber($lineNumber);

        }

    }

    public function executeStatement($statement) {

    $tokens = explode(" ", $statement);

    $command = strtoupper($tokens[0]);

    

        switch ($command) {

            case "PRINT":

                array_shift($tokens);

                $output = implode(" ", $tokens);

                $value = $this->evaluateExpression($output);

                if (is_numeric($value)) {

                    echo $value . "\n";

                } elseif (isset($this->variables[$value])) {

                    echo $this->variables[$value] . "\n";

                } else {

                    echo "Undefined variable: " . $value . "\n";

                }

                break;

            case "LET":

    $variable = $tokens[1];

    $value = $this->evaluateExpression($tokens[3]);

    $this->variables[$variable] = $value;

    break;

                

                case "INPUT":

            $variable = substr($tokens[1], 0, -1);

            echo "Enter value for $variable: ";

            echo "<form method='POST'>";

            echo "<input type='text' name='inputValue'>";

            echo "<input type='submit' value='Submit'>";

            echo "</form>";

            if ($_SERVER['REQUEST_METHOD'] === 'POST') {

                $this->input = $_POST['inputValue'];

                $this->variables[$variable] = $this->input;

                echo "Input value:" . $this->input . "<br>"; // Print the input value

            } else {

                $this->variables[$variable] = null; // Initialize the variable

            }

            break;

            

            case "GOTO":

    $lineNumber = intval($tokens[1]);

    $this->executeStatement($this->program[$lineNumber]);

    echo "Line Number: $lineNumber ";

    return;

case "THEN":

    $lineNumber = intval($tokens[1]);

    $this->executeStatement($this->program[$lineNumber]);

    echo "Line Number: $lineNumber ";

    return;

    

            

            case "GOSUB":

            $lineNumber = intval($tokens[1]);

            $this->gosubStack[] = $lineNumber;

            break;

            

            case "RETURN":

            $lineNumber = array_pop($this->gosubStack);

            break;

            

            case "IF":

    $condition = $tokens[1];

    $lineNumber = intval($tokens[4]);

echo "Line Number: $lineNumber ";

    // Evaluate the condition

    $result = $this->evaluateExpression($condition);

    if ($result) {

        $this->executeStatement($this->program[$lineNumber]);

        return;

    }

    break;

            

            case "FOR":

            //$variable = "";

            $variable = $tokens[1];

            $startValue = $this->evaluateExpression($tokens[3]);

            $endValue = $this->evaluateExpression($tokens[5]);

            $step = isset($tokens[7]) ? $this->evaluateExpression($tokens[7]) : 1;

            $this->variables[$variable] = $startValue;

            $this->forStack[] = array(

                "variable" => $variable,

                "endValue" => $endValue,

                "step" => $step,

                "lineNumber" => $lineNumber

            );

            break;

        case "NEXT":

            $variable = $tokens[1];

            $forData = end($this->forStack);

            $step = $forData["step"];

            $endValue = $forData["endValue"];

            $this->variables[$variable] += $step;

            if (($step > 0 && $this->variables[$variable] <= $endValue) ||

                ($step < 0 && $this->variables[$variable] >= $endValue)

            ) {

                $lineNumber = $forData["lineNumber"];

            } else {

                array_pop($this->forStack);

            }

            break;

            

            case "REM":

            // Ignore comments

            break;

        case "LIST":

            echo "Program listing:\n";

            ksort($this->program);

            foreach ($this->program as $line => $statement) {

                echo $line . " " . $statement . "\n";

            }

            break;

            

            case "ABS":

            //$variable = "";

            $variable = $tokens[1];

            $this->variables[$variable] = abs($this->variables[$variable]);

            break;

            

            case "INT":

            $variable = $tokens[1];

            $this->variables[$variable] = intval($this->variables[$variable]);

            break;

        case "RND":

            $variable = $tokens[1];

            $this->variables[$variable] = rand();

            break;

        case "SIZE":

            $variable = $tokens[1];

            $this->variables[$variable] = count($this->program);

            break;

            

            

            

            default:

                // Ignore unsupported commands

                break;

                //return $lineNumber; 

        } 

   // return $lineNumber; 

    }

    private function evaluateExpression($expression) {

    if ($expression === 'RND') {

        return rand();

    }

        $expression = str_replace(array_keys($this->variables), array_values($this->variables), $expression);

        return eval("return $expression;");

    }

    private function getNextLineNumber($currentLineNumber) {

        $lineNumbers = array_keys($this->program);

        $index = array_search($currentLineNumber, $lineNumbers);

        if ($index !== false && isset($lineNumbers[$index + 1])) {

            return $lineNumbers[$index + 1];

        }

        return false;

    }

}

// Example Tiny BASIC code

$code = '

1 LET Z = 1;

2 LET G = 1;

3 LET Q = 1;

5 INPUT "Z", Z;

7 PRINT "z Z";

50 PRINT "Additional print statement 1";

60 PRINT "Additional print statement 2";

70 LET Y = G;

80 PRINT "ge Y";

105 LET B = 1;

110 IF B = 1 GOSUB subject;

115 PRINT "be B";

120 subject;

125 PRINT "Hello again";

135 RETURN;

165 REM gerald rules;

170 LET A = -5;

175 ABS A;

190 PRINT "abs A";

10 LET E = 3.8;

20 INT E;

205 PRINT "int E";

207 LET T = RND;

210 PRINT "rand T";

212 LET N = 0;

215 SIZE N;

217 PRINT "sz N";

221 LET V = 0;

222 LET W = 0;

223 LET F = 0;

224 FOR F = 1 TO 10 STEP 3;

232 NEXT F;

233 FOR W = 1 TO 10 STEP 3;

234 NEXT W;

237 GOTO 240;

238 IF W THEN GOTO 240;

239 PRINT "nxt W V F";

240 PRINT "Done";

250 LIST;

310 END;

';

$code = preg_replace('/z Z/', $input, $code);

//echo $code;

$interpreter = new TinyBasicInterpreter();

$interpreter->run($code);

?>
