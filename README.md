# CHINOOK-DATASET-19-CASE-STUDY-DAY4-SQL-
Chinook-Dataset-Data-Analysis-SQL-DAY4
# 100 Days, 100 Datasets - SQL Analysis

Welcome to the repository for my "100 Days, 100 Datasets" SQL analysis project! Over the course of 100 days, I will be working with 100 different datasets to enhance my SQL skills. This repository contains the SQL queries and analyses performed on each dataset.

## Dataset for Day 4: Chinook Database

The Chinook Database is a sample database that simulates a digital media store. It contains tables for customers, invoices, tracks, albums, artists, genres, and more. This dataset is ideal for practicing complex SQL queries, including joins, aggregations, and subqueries.

### Queries and Analysis

Here is a summary of the SQL queries performed on the Chinook Database:

```sql
-- List All Customers
SELECT * FROM customer;

-- Retrieve Names and Emails of All Customers
SELECT FirstName, Email FROM customer;

-- Find Tracks with a Unit Price Greater than $0.99
SELECT * FROM track WHERE UnitPrice > 0.99;

-- List the Total Number of Invoices
SELECT COUNT(*) FROM invoice;

-- Find Names of Customers and Their Total Number of Invoices
SELECT 
    customer.FirstName, 
    COUNT(invoice.InvoiceId) AS TotalInvoices
FROM 
    customer
LEFT JOIN 
    invoice ON customer.CustomerId = invoice.CustomerId
GROUP BY 
    customer.CustomerId, customer.FirstName;

-- Get Names of All Playlists and Number of Tracks in Each Playlist
SELECT playlist.Name, COUNT(*) 
FROM playlist
LEFT JOIN playlisttrack ON playlist.PlaylistId = playlisttrack.PlaylistId
GROUP BY playlist.Name;

-- Find the Top 5 Customers Who Have Spent the Most Money
SELECT customer.FirstName, customer.CustomerId, SUM(Total) AS TotalSpent
FROM invoice
JOIN customer ON customer.CustomerId = invoice.CustomerId
GROUP BY invoice.CustomerId, customer.FirstName
ORDER BY TotalSpent DESC
LIMIT 5;

-- Retrieve List of Employees Who Support Customers, and the Number of Customers They Support
SELECT 
    employee.FirstName, 
    employee.LastName, 
    COUNT(customer.CustomerId) AS TotalCustomers
FROM 
    employee
JOIN 
    customer ON employee.EmployeeId = customer.SupportRepId
GROUP BY 
    employee.EmployeeId, employee.FirstName, employee.LastName;

-- Find Genres with the Most Tracks and Count of Tracks for Each Genre
SELECT Genre.Name, track.GenreId, COUNT(*) 
FROM track
JOIN Genre ON track.GenreId = Genre.GenreId
GROUP BY GenreId, Genre.Name;

-- Calculate Average Invoice Total for Each Country
SELECT BillingCountry, AVG(Total) 
FROM invoice
GROUP BY BillingCountry;

-- Get Names of Artists with More Than 5 Albums
SELECT 
    artist.Name, 
    COUNT(album.AlbumId) AS TotalAlbums
FROM 
    artist
JOIN 
    album ON artist.ArtistId = album.ArtistId
GROUP BY 
    artist.ArtistId
HAVING 
    COUNT(album.AlbumId) > 5;

-- Identify the Month and Year with the Highest Total Sales
SELECT DATE_FORMAT(InvoiceDate, '%Y-%m') AS YearMonth, SUM(Total) AS TotalSales
FROM invoice
GROUP BY YearMonth
ORDER BY TotalSales DESC 
LIMIT 1;

-- Find All Tracks That Are in More Than 3 Playlists
SELECT 
    track.Name, 
    COUNT(playlisttrack.PlaylistId) AS PlaylistCount
FROM 
    track
JOIN 
    playlisttrack ON track.TrackId = playlisttrack.TrackId
GROUP BY 
    track.TrackId, track.Name
HAVING 
    PlaylistCount > 3;

-- List All the Tracks That Belong to the 'Pop' Genre
SELECT 
    track.Name AS TrackName
FROM 
    track
JOIN 
    genre ON track.GenreId = genre.GenreId
WHERE 
    genre.Name = 'Pop';

-- Retrieve Details of All Employees Who Report to a Manager (SupportRepId is not NULL)
SELECT * FROM employee
WHERE ReportsTo IS NOT NULL;

-- List All the Customers from the USA
SELECT * FROM customer
WHERE Country = 'USA';

-- Find the Average Length of All Tracks
SELECT AVG(Milliseconds) / 60000.0 AS AvgTrackLengthMinutes FROM track;

-- Get the Details of the Invoice with the Highest Total
SELECT * FROM invoice
WHERE Total = (SELECT MAX(Total) FROM invoice);

-- Find the Total Sales for Each Customer by Summing Their Invoices
SELECT customer.CustomerId, SUM(Total) AS TotalSales
FROM customer
JOIN invoice ON customer.CustomerId = invoice.CustomerId
GROUP BY customer.CustomerId;

-- Identify the Most Popular Media Type by the Number of Tracks
SELECT 
    mediatype.Name AS MediaTypeName, 
    COUNT(track.TrackId) AS TotalTracks
FROM 
    mediatype
JOIN 
    track ON mediatype.MediaTypeId = track.MediaTypeId
GROUP BY 
    mediatype.MediaTypeId, mediatype.Name
ORDER BY 
    TotalTracks DESC
LIMIT 1;


## Getting Started
To explore the analyses and queries, clone this repository and review the SQL files for detailed implementations.

##bash
Copy code
git clone https://github.com/yourusername/100-days-100-datasets.git
Replace https://github.com/yourusername/100-days-100-datasets.git with the actual URL of your repository.

Feel free to reach out if you have any questions or suggestions!

