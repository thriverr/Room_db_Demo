Wishlist App

Overview

The Wishlist App is an Android application developed using Kotlin and Jetpack Compose. It allows users to create, update, and manage a wishlist. The app uses Room Database for local data storage to ensure that user data is persisted across app sessions.

Features

Add Items: Users can add new items to their wishlist.
Edit Items: Users can update or edit existing items on their wishlist.
Delete Items: Users can remove items from their wishlist.
Persist Data: All wishlist items are stored locally using Room Database.
Tech Stack

Kotlin: Programming language used for Android development.
Jetpack Compose: Android’s modern toolkit for building native UI.
Room Database: Persistence library providing an abstraction layer over SQLite to allow fluent database access.
Prerequisites

Android Studio (latest version)
Knowledge of Kotlin and Jetpack Compose
Basic understanding of Room Database
Getting Started

Installation
Clone the Repository
bash
Copy code
git clone https://github.com/thriverr/Room_db_Demo/
Open in Android Studio
Open Android Studio.
Click on File -> Open and select the cloned repository folder.
Build the Project
Click on Build -> Make Project or use the shortcut Ctrl + F9.
Running the App
Connect an Android Device or use an Emulator.
Click on Run -> Run 'app' or use the shortcut Shift + F10.
Architecture

The app follows the MVVM (Model-View-ViewModel) architecture, which helps in separating concerns and promotes a clear structure.

Components
Model: Represents the data and business logic of the app.
WishlistItem.kt: Data class representing a single wishlist item.
View: UI components built using Jetpack Compose.
MainScreen.kt: The main UI screen where wishlist items are displayed.
AddEditItemScreen.kt: UI screen for adding or editing items.
ViewModel: Manages the UI-related data in a lifecycle-conscious way.
WishlistViewModel.kt: ViewModel class managing the data and business logic for the wishlist.
Database Schema

Entity


@Entity(tableName="wish-table")
data class Wish(
    @PrimaryKey(autoGenerate = true)
    val id: Long = 0L,
    @ColumnInfo(name="wish-title")
    val title: String="",
    @ColumnInfo(name="wish-desc")
    val description:String=""
)

DAO
@Dao
abstract class WishDao {

    @Insert(onConflict = OnConflictStrategy.IGNORE)
    abstract suspend fun addAWish(wishEntity: Wish)

    // Loads all wishes from the wish table
    @Query("Select * from `wish-table`")
    abstract fun getAllWishes(): Flow<List<Wish>>

    @Update
    abstract suspend fun updateAWish(wishEntity: Wish)

    @Delete
    abstract suspend fun deleteAWish(wishEntity: Wish)

    @Query("Select * from `wish-table` where id=:id")
    abstract fun getAWishById(id:Long): Flow<Wish>


}

Database
@Database(
    entities = [Wish::class],
    version = 1,
    exportSchema = false
)
abstract class WishDatabase : RoomDatabase() {
    abstract fun wishDao(): WishDao
}

Screens

Main Screen
Displays the list of wishlist items.
Provides options to add, edit, or delete items.
Add/Edit Item Screen
Allows users to enter or modify details of a wishlist item.
Fields: Item name, description, and completion status.
Usage

Adding an Item
Click the + button on the main screen.
Fill in the item details.
Click Save to add the item to the wishlist.
Editing an Item
Tap on the item you wish to edit from the main screen.
Modify the item details.
Click Save to update the item.
Deleting an Item
Swipe the item you wish to delete from the list.
Confirm the deletion.
Contributing

Fork the repository.
Create your feature branch (git checkout -b feature/AmazingFeature).
Commit your changes (git commit -m 'Add some AmazingFeature').
Push to the branch (git push origin feature/AmazingFeature).
Open a Pull Request.
License

This project is licensed under the MIT License - see the LICENSE.md file for details.

Acknowledgements

Jetpack Compose Documentation
Room Database Documentation
Android Developers Community
