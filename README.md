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
