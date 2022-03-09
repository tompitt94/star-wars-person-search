# star-wars-person-search

Project setup
npm install

Compiles and hot-reloads for development
npm run serve

A program to search the People list from SWAPI. This displays basic information such as name, weight, height and the date the character was added to and last edited within the database.

I was going to use Axios but decided to stick with the fetch api call on this one. I created an async function to collate all the API data into one array due to pagination on the initial API responses.

There are 2 components:
  1. A filter component that allows the user to type the name of the character they wish to view
  2. A table component to display the collated data or filtered data based on the user input
