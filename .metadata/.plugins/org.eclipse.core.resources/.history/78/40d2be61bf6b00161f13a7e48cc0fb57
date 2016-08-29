package com.weekfourproject;

import java.sql.*;
import java.util.ArrayList;
import java.util.Scanner;

public class DAO 
{
	static final String DB_URL = "jdbc:mysql://localhost:3306/?user=root&autoReconnect=true&useSSL=false";
	static final String USER = "root";
	static final String PASSWORD = "root";
	
	static Connection CONN= null;
	static Statement STMT= null;
	static PreparedStatement PREP_STMT = null;
	static ResultSet RES_SET= null;
	
	static Scanner sc = new Scanner(System.in);
	
	public static void connToDB()
	{
		try 
		{
			System.out.println("Connecting to the Database");
			CONN = DriverManager.getConnection(DB_URL, USER, PASSWORD);
			System.out.println("Connected to the database");
		}
		
		catch (SQLException e) 
		{
		System.out.println("Failed to connect to the database.");
		e.printStackTrace();
		}
	}
	
	public static void readFromDB() 
	{
		connToDB();
		
		ArrayList<Movie> ourMovies = new ArrayList<>();
		try
		{
			STMT = CONN.createStatement();
			RES_SET = STMT.executeQuery("SELECT * FROM movies.movies;");
			
			while(RES_SET.next())
			{
				Movie movietInDB = new Movie();
				movietInDB.setMovieID(RES_SET.getString("movie_id"));
				movietInDB.setMovieTitle(RES_SET.getString("title"));
				movietInDB.setMovieRating(RES_SET.getString("rating"));
				movietInDB.setMovieGenre(RES_SET.getString("genre"));
				movietInDB.setMovieLength(RES_SET.getInt("length"));
				
				ourMovies.add(movietInDB);
			}
			
			for(Movie Movie : ourMovies)
			{
				System.out.println(Movie.toString());
			}
			
		}
		catch(SQLException e)
		{
			e.printStackTrace();
		}
	}
	
	public static void writeToDB()
	{
		Movie movieToAdd = new Movie();
		
		movieToAdd = aboutTheMovie();
		
		connToDB();
		
		try 
		{
			PREP_STMT = CONN.prepareStatement(insertToDatabase);
			
			PREP_STMT.setString(1, movieToAdd.getMovieTitle());
			PREP_STMT.setString(2, movieToAdd.getMovieRating());
			PREP_STMT.setString(3, movieToAdd.getMovieGenre());
			PREP_STMT.setInt(4, movieToAdd.getMovieLength());
			
			PREP_STMT.executeUpdate();
		} 
		
		catch (SQLException e) 
		{
			e.printStackTrace();
		}
	}
	
	private static String insertToDatabase = "INSERT INTO `movies`.`movies`"
			+ "(title, rating, genre, length)"
			+ "VALUES"
			+ "(?, ?, ?, ?)";
	
	private static Movie aboutTheMovie()
	{
		Movie movieToAdd = new Movie();
		
		System.out.println("What is the title of the movie?");
		movieToAdd.setMovieTitle(sc.nextLine());
		
		System.out.println("What is the movie's rating?");
		movieToAdd.setMovieRating(sc.nextLine());
		
		System.out.println("What is the movie's genre?");
		movieToAdd.setMovieGenre(sc.nextLine());
		
		System.out.println("What is the length of the movie in minutes?");
		movieToAdd.setMovieLength(Integer.parseInt(sc.next()));
		
		return movieToAdd;
		
	}
	
	private static String deleteFromDatabase = "DELETE FROM `movies`.`movies`"
			+ "Where"
			+ "(title)"
			+ " = (?)";
	
	private static Movie aboutTheMovieToBeDeleted()
	{
		Movie movieToDelete = new Movie();
		
		System.out.println("Enter the movie's title that you want to delete");
		movieToDelete.setMovieTitle(sc.nextLine());
		
		return movieToDelete;
	}
	
	public static void deleteToDatabase()
	{
		Movie movieToDelete = new Movie();
		movieToDelete = aboutTheMovieToBeDeleted();
		connToDB();
		
		try 
		{
			PREP_STMT = CONN.prepareStatement(deleteFromDatabase);
			PREP_STMT.setString(1, movieToDelete.getMovieTitle());
			PREP_STMT.executeUpdate();
		} 
		
		catch (Exception e) 
		{
			e.printStackTrace();
		}
		
	}
	
	private static String modifyFromDB = "UPDATE `movies`.`movies`"
            + "SET"
            +" title= ?, rating= ?, genre= ?, length= ?"
            + " WHERE "
            + "`title`"
            + "= ?";
			
	private static Movie aboutTheMovieModified()
	{
		Movie movieToModify = new Movie();
		
		System.out.println("What is the title of the updated movie?");
		movieToModify.setMovieTitle(sc.nextLine());
		
		System.out.println("What is the movie's updated rating?");
		movieToModify.setMovieRating(sc.nextLine());
		
		System.out.println("What is the movie's updated genre?");
		movieToModify.setMovieGenre(sc.nextLine());
		
		System.out.println("What is the updated length of the movie in minutes?");
		movieToModify.setMovieLength(Integer.parseInt(sc.next()));
		
//		System.out.println("What is the movie's original title?");
//		movieToModify.setMovieTitle(sc.nextLine());
		
		return movieToModify;
		
	}
	
	public static void modifyToDB()
	{
		Movie movieToModify = new Movie();
		movieToModify=aboutTheMovieModified();
		connToDB();
		
		try 
		{
			PREP_STMT = CONN.prepareStatement(modifyFromDB);
			
			PREP_STMT.setString(1, movieToModify.getMovieTitle());
			PREP_STMT.setString(2, movieToModify.getMovieRating());
			PREP_STMT.setString(3, movieToModify.getMovieGenre());
			PREP_STMT.setInt(4, movieToModify.getMovieLength());
			PREP_STMT.setString(5, movieToModify.getMovieTitle());
			
			PREP_STMT.executeUpdate();
		} 
		
		catch (SQLException e) 
		{

			e.printStackTrace();
		}
		
	}
}