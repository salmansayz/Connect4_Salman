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
