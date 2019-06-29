Github Gists PHP API
=======

Github Gists PHP API is a light-weight object Oriented wrapper for Github Gist API.

Github Gists PHP API ist ein leichtgewichtiger objektorientierter Wrapper für die Github Gist API.

  - Required: **PHP 5 or higher**
  - Uses **Github API v3**
  - **Easy to Use Helper Class** for updating Gists
  
  
  - Erforderlich: **PHP 5 oder höher**
  - Verwendet **Github API v3**
  - **Einfach zu bedienende Helferklasse** für die Aktualisierung der Gists



# Demo

```php
require_once('_PATH_/gists_api.php');

$gistAPI = new gistAPI($github_ID, $github_Password);
```
```php
// Program to get a Gist.
$ouput = $gistAPI->getGist(":gist_Id");
```
```php
// Program to Edit a Gist Using The Helper Class.

$filesArray = GistEdit::init()
                ->newFile("file1.txt" => "File1 Content")
                ->newFile("file2.txt" => "File2 Content")
                ->newFile("file3.txt" => "File3 Content");
                
$ouput = $gistAPI->createGist($filesArray);
```

# Functions
# Funktionen

Basic Usage
Grundlegende Verwendung
------------

```php
require_once('_PATH_/gists_api.php');

$gistAPI = new gistAPI(); //To Authenticate anonymous / So authentifizieren Sie sich anonym


// To Authenticate with Github Username and Password
// So authentifizieren Sie sich mit Github-Benutzername und Passwort
$gistAPI = new gistAPI($github_ID, $github_Password);

```

## API Limits
```php
//Get the remainning API request limits left.
$limits = $gistAPI->getLimits();

```

## Gists

### List Gists

```php
//Display All Public Gists
$Gists = $gistAPI->listGists("public");

//Displays gists of account of username "someUsername" 
//Displays Authenticated user's gists if second atribute not given
$Gists = $gistAPI->listGists("user", ":someUsername");

//Displays gists starred by the authenticated User
$Gists = $gistAPI->listGists("starred");
```

### Get single Gist
```php
//Display a single Gist using gist's ID
$Gist = $gistAPI->getGist(":gist_id");

```

### Create a Gist
### Erstellen Sie ein Gist
```php
//Create a new Secret Gist with a Description
//Erstellen eines neuen Geheimen Gist mit einer Beschreibung
function create_githubgist($title, $text, $public = false) {

    global $gistAPI;

    //Create A New Secret Gist
    //Erstelle einen neuen geheimen Gist
    $newGist = $gistAPI->createGist($title.'.article', 'Created by TEST', $text, $public);

    return $newGist;

}

    //Create A New Secret Gist
    //Erstelle einen neuen geheimen Gist
$newGist = create_githubgist('TITLETEST', 'TEXT TEST', false);

// Echo Test
echo '<pre>' . var_export($newGist, true) . '</pre>';
echo $newGist['body']['html_url'];
```
### Edit a Gist
```php

function edit_githubgist($title, $text) {

    global $gistAPI;
    
    //Edit The File And Description And Content
    //Bearbeiten der Datei und Beschreibung und Inhalt
    $editGist = $gistAPI->editGist(":gist_id", $title.'.article', $title, $text); 

    return $editGist;

}

$newGist = edit_githubgist('TITLEEDITTEST', 'TEXT TEST EDIT');

// Echo Test
echo '<pre>' . var_export($newGist, true) . '</pre>';
echo $newGist['body']['html_url'];
```
### List Gist Commits
```php
// Display gist's Commits
$commits = $gistAPI->gistCommits(":gist_id");
```
### Star a Gist
```php
// Star a Gist
$star = $gistAPI->starGist(":gist_id");
```
### Unstar a Gist
```php
// Unstar a Gist
$unstar = $gistAPI->unstarGist(":gist_id");
```
### Check if Gist is starred
```php
// Star a Gist
$checkStar = $gistAPI->checkStarGist(":gist_id");
```
### Fork a Gist
```php
// Fork a Gist
$fork = $gistAPI->forkGist(":gist_id");
```
### List Gist Forks
```php
// Displays all Forks of the Gist
$listForks = $gistAPI->listForkGist(":gist_id");
```
### Delete a Gist
```php
// Delete a Gist
// Lösche einen Gist
$delete = $gistAPI->deleteGist(":gist_id");

if(preg_match('/^204 No Content/im', $delete['header']['Status'])) {
    echo "Success";
} else {
	echo "Failed";
}
```
## Comments

### List comments on a gist
```php
// Display all the Comments of a particular Gist
$comments = $gistAPI->gistComments(":gist_id");
```
### Get a single comment
```php
// Display a particular Comments of a particular Gist.
$comment = $gistAPI->getComment(":gist_id", ":comment_id");
```
### Create a comment
```php
// Create a new Comment in a Gist
$newComment = $gistAPI->createComment(":gist_id", "Some Random Comment Data");
```
### Edit a comment
```php
// Edit a comment of a Gist
$editComment = $gistAPI->editComment(":gist_id", ":coment_id", "New Comment Data");
```

### Delete a comment
```php
// Delete a comment of a Gist
$deleted = $gistAPI->editComment(":gist_id", ":coment_id");
```

Edit Helper Class
-------
## Basic Usage
```php
// Its Common in All Queries
$filesArray = GistEdit::init();
// Note: GistEdit being a static class. Hence NO NEED to initiate it by 
//          $GistEdit = new GistEdit();
```

### Create A New File

```php
// Add a New file to the filesArray
$filesArray = GistEdit::init()->newFile("newfilename.txt", "Some Content");
// Note: The following command can be chained with other GistEdit functions.
```
### Edit a  File

```php

// Edit a filename and its Content In the filesArray
$filesArray = GistEdit::init()->edit("filename.txt", "New Content", "new_filename.txt");

// Edit only file Content In the filesArray
$filesArray = GistEdit::init()->edit("filename.txt", "New Content");

// Edit only filename In the filesArray
$filesArray = GistEdit::init()->edit("filename.txt", NULL, "new_filename.txt");

// Note: The following command can be chained with other GistEdit functions.
```

### Delete a File

```php
// Delete a file In the filesArray
$filesArray = GistEdit::init()->deleteFile("filename.txt");
// Note: The following command can be chained with other GistEdit functions.
```
