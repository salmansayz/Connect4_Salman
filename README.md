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
