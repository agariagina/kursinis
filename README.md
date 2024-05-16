# Movie theatre management system
## Introduction
### What is your application?
The Movie Theater Management System is a Python application designed to manage movie data and ticketing for a theater. The application imports movie data from an existing Excel file, allows users to view the movies currently playing, and generates tickets for specific movies. This application demonstrates various object-oriented programming principles such as abstraction, encapsulation, the singleton pattern, and the factory method pattern.
### How to run the program?
1) Ensure that you have Python installed on your system.
2) Install the required Python libraries.
3) Place your Excel file containing movie data (movies.xlsx) in the same directory as your script.
4) Save the provided Python code into a file.
5) Run the script.
### How to use the program?
* The program reads the movie data from movies.xlsx and displays the movies playing at the theater.
* It creates ticket objects for specified movies and exports ticket data to a CSV file.
* Users can run the script to view the movie information and generate tickets for viewing purposes.
## Body/Analysis
### Analysis and explanation of the program's implementation
The application consists of several components that demonstrate the use of object-oriented programming principles.
### Abstraction and Encapsulation
The Movie and Ticket classes encapsulate the properties and methods relevant to movies and tickets.


class Movie:

    def __init__(self, title, genre, duration):
        self.title = title
        self.genre = genre
        self.duration = duration

    def get_info(self):
        return f"Title: {self.title}, Genre: {self.genre}, Duration: {self.duration} mins"

class Ticket:

    def __init__(self, movie, seat_number, price):
        self.movie = movie
        self.seat_number = seat_number
        self.price = price
    
    def get_ticket_info(self):
        return f"Movie: {self.movie.title}, Seat Number: {self.seat_number}, Price: ${self.price: .2f}"

### Singleton Pattern
The Theater class uses the singleton pattern to ensure that there is only one instance of the theater.

class Theater:

    _instance = None
    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = super(Theater, cls).__new__(cls)
            cls._instance.movies = []
        return cls._instance
    
    def add_movie(self, movie):
        self.movies.append(movie)

    def show_movies(self):
        print(f"Movies playing at the theater:")
        for movie in self.movies:
            print(movie.get_info())


### Factory Method Pattern
The TicketFactory class uses the factory method pattern to create ticket objects.

class TicketFactory:

    @staticmethod
    def create_ticket(movie, seat_number, price):
        return Ticket(movie, seat_number, price)


### Data Import/Export
The DataHandler class handles the import of movie data from an Excel file and the export of ticket data to a CSV file.

class DataHandler:

    @staticmethod
    def import_movies_from_excel(filename):
        movies = []
        df = pd.read_excel(filename)
        for _, row in df.iterrows():
            movies.append(Movie(row['title'], row['genre'], int(row['duration'])))
        return movies
    
    @staticmethod
    def export_tickets_to_csv(tickets, filename):
        with open(filename, 'w', newline='') as file:
            writer = csv.writer(file)
            writer.writerow(['Movie Title', 'Seat Number', 'Price'])
            for ticket in tickets:
                writer.writerow([ticket.movie.title, ticket.seat_number, ticket.price])

## Results and Summary
### Results
* The program successfully imports movie data from an Excel file and displays the movies playing at the theater.
* Ticket objects are created for specific movies and exported to a CSV file.
* The use of object-oriented principles enhances the modularity and readability of the code.

### Challenges
* Ensuring that the singleton pattern is correctly implemented to maintain a single instance of the Theater class.
* Handling the import of movie data from Excel and ensuring correct data parsing.

## Conclusions
### Key Findings and Outcomes
* The application demonstrates effective use of object-oriented principles in Python.
* It provides a functional example of managing movie data and ticketing for a theater.
* The program achieves its goal of importing movie data, displaying it, and generating tickets.

### Future Prospects
* Extend the application to support more complex ticketing features, such as seat selection and different pricing tiers.
* Implement a user interface for easier interaction with the application.
* Integrate with a database for persistent storage of movie and ticket data.


