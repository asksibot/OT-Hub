OT-Hub Books
This repository provides a curated list of books and resources designed for occupational therapy, personal development, mental health, and sensory integration. The collection is organized with filters for specific audiences and topics, making it easy to integrate into various webpages such as asksibot.org.

Table of Contents
Setup
Structure and Attributes
Usage
Integrating the Book List
Applying Filters
Clearing Filters
Keyword Search
Updating the Book List
Example Code
Troubleshooting
Setup
Clone or Download the Repository
Clone this repository to your local machine or download it as a .zip file.

bash
Copy code
git clone https://github.com/your-username/ot-hub-books.git
Add to Your Website
Include the HTML and JavaScript code snippets provided in this repository within your desired webpage.

Link the JavaScript File
If the JavaScript for filtering and search functions is separate, ensure it is linked in the <head> section of your HTML file:

html
Copy code
<script src="path/to/filter.js"></script>
Structure and Attributes
Each book in the list uses custom data-audience and data-condition attributes to enable filtering by audience and topic.

Example Book Item
html
Copy code
<li data-audience="individual therapist" data-condition="mental-health emotional-healing">
    <strong>Writing as a Way of Healing</strong> by Louise DeSalvo
    <p>This book highlights the therapeutic benefits of writing for self-healing.</p>
</li>
Audience and Condition Tags
Audience Tags: These identify the target audience (e.g., individual, therapist, caregiver, parent-guardian, etc.)
Condition Tags: These describe the main topics of the book (e.g., mental-health, nutrition, autism-spectrum, executive-functioning, etc.)
Usage
Integrating the Book List
To integrate the book list, copy the HTML structure for each category section and add it to your desired page. Each section should include:

Filters for Audience and Condition: Dropdown menus for filtering by data-audience and data-condition.
Book List: The <ul> elements containing each <li> book item.
Applying Filters
Audience and Condition Filters: Use dropdowns or checkboxes to select audience and condition filters.
JavaScript Function: The applyFilters() function allows users to filter books within each section.
Example:

javascript
Copy code
function applyFilters(section) {
    const audienceFilter = document.getElementById(`audience-filter-${section}`).value;
    const conditionFilter = document.getElementById(`condition-filter-${section}`).value;
    const bookItems = document.querySelectorAll(`#${section} ul li`);

    bookItems.forEach(book => {
        const audience = book.getAttribute('data-audience');
        const condition = book.getAttribute('data-condition');
        const matchesAudience = !audienceFilter || audience.includes(audienceFilter);
        const matchesCondition = !conditionFilter || condition.includes(conditionFilter);

        book.style.display = matchesAudience && matchesCondition ? 'block' : 'none';
    });
}
Clearing Filters
Each section includes a Clear Filters button, which resets all filters and displays the full list.

javascript
Copy code
function clearFilters(section) {
    document.getElementById(`audience-filter-${section}`).value = "";
    document.getElementById(`condition-filter-${section}`).value = "";
    const bookItems = document.querySelectorAll(`#${section} ul li`);
    bookItems.forEach(book => {
        book.style.display = 'block';
    });
}
Keyword Search (Optional)
To add a keyword search, create an input field for keywords and a function to filter books based on title or description.

html
Copy code
<input type="text" id="search-keyword" placeholder="Search by keyword">
<button onclick="searchBooks('section')">Search</button>
javascript
Copy code
function searchBooks(section) {
    const keyword = document.getElementById('search-keyword').value.toLowerCase();
    const bookItems = document.querySelectorAll(`#${section} ul li`);
    
    bookItems.forEach(book => {
        const title = book.querySelector('strong').textContent.toLowerCase();
        const description = book.querySelector('p').textContent.toLowerCase();
        book.style.display = title.includes(keyword) || description.includes(keyword) ? 'block' : 'none';
    });
}
Updating the Book List
Adding New Books
Each new book should be added as an <li> element within the relevant <ul> section. Use appropriate data-audience and data-condition attributes.

Editing Attributes
To update an existing book's audience or topics, edit the values within its data-audience and data-condition attributes.

Removing Books
Simply delete the <li> item for the book you wish to remove.

Example Code
Here’s a complete example of a section with filters and book list:

html
Copy code
<div class="filter-section">
    <h2>Personal Growth & Relationships</h2>
    <label for="audience-filter-growth">Select Audience:</label>
    <select id="audience-filter-growth">
        <option value="">All</option>
        <option value="individual">Individual</option>
        <option value="therapist">Therapist</option>
    </select>

    <label for="condition-filter-growth">Select Condition:</label>
    <select id="condition-filter-growth">
        <option value="">All</option>
        <option value="marriage-relationships">Marriage & Relationships</option>
        <option value="self-help">Self-Help</option>
    </select>

    <div class="filter-buttons">
        <button onclick="applyFilters('growth')">Apply Filters</button>
        <button onclick="clearFilters('growth')">Clear Filters</button>
    </div>

    <div class="book-category" id="personal-growth">
        <ul>
            <li data-audience="individual" data-condition="marriage-relationships self-help">
                <strong>The Seven Principles for Making Marriage Work</strong> by John M. Gottman, Ph.D., and Nan Silver
                <p>A guide outlining seven principles for a healthy marriage...</p>
            </li>
            <!-- Add more books here -->
        </ul>
    </div>
</div>
Troubleshooting
Books Not Filtering Correctly

Ensure data-audience and data-condition attributes are correctly set.
Confirm that IDs for dropdowns and buttons match those used in the JavaScript functions.
Clear Filters Not Working

Check the clearFilters() function and ensure it is called with the correct section name.
JavaScript Errors

Open the console (usually F12 in your browser) to view any JavaScript errors. Make sure all IDs and selectors match.
