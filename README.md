private Color winner;
public static final int DISCS_FOR_WIN = 4;
public void putDisc(int column) {

if (numOfDiscs < ROWS) {
board[column - 1][numOfDiscs] =
currentPlayer;
printBoard();
checkWinCondition(column – 1,
numOfDiscs);
switchPlayer();
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
}
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
}
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
.matches()) 
{
winner = currentPlayer;
System.out.println(currentPlayer +
" wins");
}
}
