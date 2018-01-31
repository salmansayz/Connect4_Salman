# Connect4_Salman
//Condition1
public class Connect4 {
public enum Color {
RED('R'), GREEN('G'), EMPTY(' ');
private final char value;
Color(char value) { this.value = value; }
@Override
public String toString() {
return String.valueOf(value);
}
}
public static final int COLUMNS = 7;
public static final int ROWS = 6;
private Color[][] board = new Color[COLUMNS][ROWS];
public Connect4() {
for (Color[] column : board) {
Arrays.fill(column, Color.EMPTY);
}
}
}
//Condition2
public void putDisc(int column) {
if (column > 0 && column <= COLUMNS) {
int numOfDiscs =
getNumberOfDiscsInColumn(column - 1);
if (numOfDiscs < ROWS) {
board[column - 1][numOfDiscs] =
Color.RED;
}
}
}
private int getNumberOfDiscsInColumn(int column) {
if (column >= 0 && column < COLUMNS) {
int row;
for (row = 0; row < ROWS; row++) {
if (Color.EMPTY == board[column][row]) {
return row;
}
}
return row;
}
return -1;
}
//Condition3
private Color currentPlayer = Color.RED;
private void switchPlayer() {
if (Color.RED == currentPlayer)
currentPlayer = Color.GREEN;
} else {
currentPlayer = Color.RED;
}
}
public void putDisc(int column) {
if (column > 0 && column <= COLUMNS) {
int numOfDiscs =
getNumberOfDiscsInColumn(column - 1);
if (numOfDiscs < ROWS) {
board[column - 1][numOfDiscs] =
currentPlayer;
switchPlayer();
}
}
}
//Condition4
public boolean isFinished() {
int numOfDiscs = 0;
for (int col = 0; col < COLUMNS; ++col) {
numOfDiscs +=
getNumberOfDiscsInColumn(col);
}
if (numOfDiscs >= COLUMNS * ROWS) {
System.out.println("It's a draw");
return true;
}
return false;
}
//Condition5
private Color winner;
public static final int DISCS_FOR_WIN = 4;
public void putDisc(int column) {
...
if (numOfDiscs < ROWS) {
board[column - 1][numOfDiscs] =
currentPlayer;
printBoard();
checkWinCondition(column – 1,
numOfDiscs);
switchPlayer();
...
}
private void checkWinCondition(int col, int row) {
Pattern winPattern =
Pattern.compile(".*" + currentPlayer +
"{" + DISCS_FOR_WIN + "}.*");
// Vertical check
StringJoiner stringJoiner =
new StringJoiner("");
for (int auxRow = 0; auxRow < ROWS; ++auxRow) {
stringJoiner
.add(board[col][auxRow].toString());
}
if (winPattern.matcher(stringJoiner.toString())
.matches()) {
winner = currentPlayer;
System.out.println(currentPlayer +
" wins");
}
}
public boolean isFinished() {
if (winner != null) return true;
...
}
private void checkWinCondition(int col, int row) {
...
// Horizontal check
stringJoiner = new StringJoiner("");
for (int column = 0; column < COLUMNS;
++column) {
stringJoiner
.add(board[column][row].toString());
}
if (winPattern.matcher(stringJoiner.toString())
.matches()) {
winner = currentPlayer;
System.out.println(currentPlayer +
" wins");
return;
}
...
}
private void checkWinCondition(int col, int row) {
...
// Diagonal checks
int startOffset = Math.min(col, row);
int column = col - startOffset,
auxRow = row - startOffset;
stringJoiner = new StringJoiner("");
do {
stringJoiner
.add(board[column++][auxRow++].toString());
} while (column < COLUMNS && auxRow < ROWS);
if (winPattern.matcher(stringJoiner.toString())
.matches()) {
winner = currentPlayer;
System.out.println(currentPlayer +
" wins");
return;
}
startOffset = Math.min(col, ROWS - 1 - row);
column = col - startOffset;
auxRow = row + startOffset;
stringJoiner = new StringJoiner("");
do {
stringJoiner
.add(board[column++][auxRow--].toString());
} while (column < COLUMNS && auxRow >= 0);
if (winPattern.matcher(stringJoiner.toString())
.matches()) {
winner = currentPlayer;
System.out.println(currentPlayer +
" wins");
}
}
