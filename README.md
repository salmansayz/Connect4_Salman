package com.path.fms.actions.applicationfacility;

import java.util.Arrays;
import java.util.StringJoiner;
import java.util.regex.Pattern;

public class Connect4
{
    int numOfDiscs = 0;
    private Color currentPlayer = Color.RED;
    Pattern winPattern = Pattern.compile(".*" + currentPlayer + "{" + DISCS_FOR_WIN + "}.*");

    public static final int COLUMNS = 7;
    public static final int ROWS = 6;
    private static Color[][] board = new Color[COLUMNS][ROWS];
    private static final String DELIMITER = "|";

    public static void main()
    {
	for(Color[] column : board)
	{
	    Arrays.fill(column, Color.EMPTY);
	}
    }

    public enum Color
    {
	RED('R'), GREEN('G'), EMPTY(' ');
	private final char value;

	Color(char value)
	{
	    this.value = value;
	}

	@Override
	public String toString()
	{
	    return String.valueOf(value);
	}
    }

    public Connect4()
    {
	for(Color[] column : board)
	{
	    Arrays.fill(column, Color.EMPTY);
	}
    }


    // Condition2
    public void putDisc(int column)
    {
	if(column > 0 && column <= COLUMNS)
	{
	    int numOfDiscs = getNumberOfDiscsInColumn(column - 1);
	    if(numOfDiscs < ROWS)
	    {
		board[column - 1][numOfDiscs] = Color.RED;
	    }
	}
    }

    private int getNumberOfDiscsInColumn(int column)
    {
	if(column >= 0 && column < COLUMNS)
	{
	    int row;
	    for(row = 0; row < ROWS; row++)
	    {
		if(Color.EMPTY == board[column][row])
		{
		    return row;
		}
	    }
	    return row;
	}
	return -1;
    }

    // Condition3


    private void switchPlayer()
    {
	if(Color.RED == currentPlayer)
	{
	    currentPlayer = Color.GREEN;
    }else

    {
	currentPlayer = Color.RED;
    }
    }

    public void putDisc1(int column)
    {
	if(column > 0 && column <= COLUMNS)
	{
	    int numOfDiscs = getNumberOfDiscsInColumn(column - 1);
	    if(numOfDiscs < ROWS)
	    {
		board[column - 1][numOfDiscs] = currentPlayer;
		switchPlayer();
	    }
	}
    }

    // Condition4
    public boolean isFinished()
    {

	for(int col = 0; col < COLUMNS; ++col)
	{
	    numOfDiscs += getNumberOfDiscsInColumn(col);
	}
	if(numOfDiscs >= COLUMNS * ROWS)
	{
	    System.out.println("It's a draw");
	    return true;
	}
	return false;
    }

    // Condition5
    private Color winner;
    public static final int DISCS_FOR_WIN = 4;

    // public void putDisc2(int column) {
    // if (numOfDiscs < ROWS) {
    // board[column - 1][numOfDiscs] =
    // currentPlayer;
    // printBoard();
    // checkWinCondition(column– 1,
    // numOfDiscs);
    // switchPlayer();
    // }

    // private void printBoard()
    // {
    // for(int row = ROWS - 1; row >= 0; row--)
    // {
    // StringJoiner stringJoiner = new StringJoiner(DELIMITER, DELIMITER,
    // DELIMITER);
    // Stream.of(board[row]).forEachOrdered(stringJoiner::add);
    // outputChannel.println(stringJoiner.toString());
    // }
    // }

    private void checkWinCondition(int col, int row)
    {
	// Vertical check
	StringJoiner stringJoiner = new StringJoiner("");
	for(int auxRow = 0; auxRow < ROWS; ++auxRow)
	{
	    stringJoiner.add(board[col][auxRow].toString());
	}
	if(winPattern.matcher(stringJoiner.toString()).matches())
	{
	    winner = currentPlayer;
	    System.out.println(currentPlayer + " wins");
	}
    }

    public boolean isFinished1() {
	if(winner != null)
	{
	    return true;
	}
	else
	{
	    return false;
	}
    }

    private void checkWinCondition1(int col, int row) {
	            // Horizontal check
	StringJoiner stringJoiner = new StringJoiner("");
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

    private void checkWinCondition2(int col, int row) {
	            // Diagonal checks
	            int startOffset = Math.min(col, row);
	            int column = col - startOffset,
	            auxRow = row - startOffset;
	StringJoiner stringJoiner = new StringJoiner("");
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

}
