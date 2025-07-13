### Prep-Time: Your Personal Flashcard System
Prep-Time is a dynamic and intuitive web application designed to help users create, manage, and review their own custom flashcard sets. Whether you're studying for an exam, learning a new language, or just organizing information, Prep-Time provides a streamlined experience for effective learning.

## Overview
This application functions as a comprehensive flashcard system, enabling users to:
- Create and manage multiple flashcard sets.
- Add, edit, and delete individual flashcards within any given set.
- Save and review sets at their convenience, fostering continuous learning.

The application leverages React for a responsive and interactive frontend, with React Router DOM handling seamless navigation between different sections of the application.

# Architecture and Structure
The Prep-Time application is built around two primary React components, ensuring a clear separation of concerns and maintainability:

FlashcardSets Component:
- This serves as the main entry point for managing flashcard collections.
- Users can create new flashcard sets and view a list of all existing sets here.
- It acts as the central hub for set-level operations.

Flashcards Component:
- This component is dedicated to the detailed management of flashcards within a specific set.
- Users navigate to this page to add new flashcards, or to edit and delete existing ones.

# How It Works: A User Flow
- Homepage Access: From the navigation bar, users can click "Flashcard Sets" to access the main set management page.
- Set Creation: On the FlashcardSets page, users can type a desired name into an input field and click "Add Set" to create a new flashcard collection. The input field then resets.
- Navigating to a Set: Each created set is displayed as a clickable item. Clicking on a set's visual representation navigates the user to the Flashcards page, using the set's unique ID embedded in the URL.

# Flashcard Management (within Flashcards Component):
- Adding Flashcards: Users can input a question and an answer into designated fields. Clicking "Add Flashcard" saves this new flashcard to the currently active set.
- Editing Flashcards: Clicking "Edit" on an existing flashcard populates the input fields with its current question and answer. After making changes, clicking "Update Flashcard" saves these modifications.
- Deleting Flashcards: A "Delete" button allows users to remove individual flashcards from the set.
- Saving and Reviewing: Once done managing flashcards, users can click "Review Set." This action sends the current set's data to a server (via a POST request) for persistence and then navigates the user to a dedicated review page.

# Key React Features & Implementation Details
State Management with useState:
- The application extensively uses the useState hook to manage dynamic data, including the comprehensive list of flashcardSets, the name of a new set being created (setName), input values for flashcard questions/answers, and the edit states of individual flashcards.
- When a new set is added, it's pushed into the flashcardSets array with a unique ID and an initially empty list for its flashcards.
  
Dynamic Routing with react-router-dom:
- The useNavigate hook is employed to programmatically navigate users between different pages (e.g., from FlashcardSets to Flashcards).
- The useParams hook is utilized to extract URL parameters, such as the setID, which is crucial for fetching and displaying the correct flashcard set on the Flashcards page.

Component Props for Data Flow:
- Data is efficiently passed from parent components to child components using props.
- For instance, the FlashcardSets component receives flashcardSets (the array of all sets) and setFlashcardSets (the state update function) as props from App.js. This allows FlashcardSets to both access the global list of sets and trigger updates to that list when new sets are added.
- The setFlashcardSets function, passed down as a prop, ensures that any additions, edits, or deletions of flashcards or sets are reflected globally across the application's state, maintaining data consistency.

Design Rationale
- The architectural decision to divide the application into distinct FlashcardSets and Flashcards components, coupled with a centralized state management in the parent App.js, significantly enhances the application's maintainability and scalability. This modular approach makes it easier to debug, add new features, and understand the flow of data within the application.
