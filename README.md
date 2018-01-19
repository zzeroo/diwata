# Diwata 
Diwata is a database interface for PostgreSQL with the goal of being usable, user-friendly with its basic and advanced functionality be discoverable by the user.
Goal of diwata is to be a replacement of back-end admin without explicitly writing the code for it.[1]
It is content aware, and renders records as it sees fits.
An attempt to create back-end to end all back-ends.

[![](https://travis-ci.org/ivanceras/diwata.svg?branch=master)](https://travis-ci.org/ivanceras/diwata)


![](https://raw.githubusercontent.com/ivanceras/diwata/master/diwata1.png)
![](https://github.com/ivanceras/ivanceras.github.io/blob/master/diwata/diwata3.png)
![](https://github.com/ivanceras/ivanceras.github.io/blob/master/diwata/diwata4.png)


## Features
- Automatic display of direct and indirect linked record
- Freeze column and freeze rows
- Infinite scrolling / loading of page on scrolling
- User friendly granular search and filter
- Diplay descriptive referred records. (ie: Instead of displaying the foreign_key value integer or uuid, display the referred records in such a way it is distinguisable by the user)

Freeze row
![](https://raw.githubusercontent.com/ivanceras/ivanceras.github.io/master/diwata/diwata-freeze-row.gif)
Freeze column
![](https://raw.githubusercontent.com/ivanceras/ivanceras.github.io/master/diwata/diwata-freeze-column.gif)

Distinguisable referred record in a dropdown
![](https://raw.githubusercontent.com/ivanceras/ivanceras.github.io/master/diwata/meaningful-dropdown.gif)

Dynamic toolbar displaying the exact information of what the button actually does
![](https://raw.githubusercontent.com/ivanceras/ivanceras.github.io/master/diwata/dynamic-toolbar.gif)

### [Sakila Demo](http://web01.jcesar.clh.no:8000)

### Needed Dependencies
- elm v0.18 ( elm installation needed npm or yarn)
- rsync  ( for fast syncing files over and over )
- google-closure-compiler (optional, for release build)
- sed (search and replace `app.js` with `app.min.js` in `index.html`
- sakila database (for demo and testing) [2]

## Install Dependencies 
```sh
sudo apt install rsync
npm install -g elm@0.18
npm install -g google-closure-compiler-js

```


Compile and run 
```
git clone https://github.com/ivanceras/diwata
cd diwata
rustup override set nightly-2017-12-21
cd webclient && ./compile.sh && cd ..

cargo run -p diwata -- --dburl <db_url>

```
Note: Needed to use specific nightly until [this montogmery issue is resolved](https://github.com/rust-lang/rust/issues/46936)

## Specify a database ( sakila database example )

```
cargo run -p diwata -- --dburl postgres://postgres:passwd@localhost:5432/sakila
```
see `run.sh` for the accurate content of command

Then visit http://localhost:8000/

## Content Aware
Using heristic method, diwata is able to infer the content of a table.
- When it a column is a boolean it make sense to display it with a checkbox rather than just 'true' and 'false'
    Dates will be rendered with a dropdown calender.
- Country lookup will be rendered with a dropdown list of country alongside their flags 
- Images will be displayed in line when in grid view, and will be fully displayed when in card view
- Attachments such as pdf,xls,csv,svg,md,txt,source codes will be rendered to their corresponding document editors
- Urls are linked and clickable automatically
- Embed common web objects: youtube videos, tweets, images, map locations
- tags are rendered as such

Roadmap checklist:
- [X] Infinite load-on-deman scrolling
- [X] Meaningful dropdown lookup
- [ ] Delete records
- [ ] Update records
- [ ] Insert records
- [ ] Undo update/delete records
- [X] Search and filter data
- [ ] Drag and resize columns
- [ ] Multi column sorting
- [ ] Smart delete cascade messages
- [ ] Error messages display
- [X] Interactive/dynamic record count indicator for toolbar buttons
- [X] Loading indicator
- [ ] Page transition animation

Notes:
[1]: This has been tried before (compiere, adempiere, openbravo, salesforce) etc.
[2]: You can use sakila database dump as demo database https://github.com/ivanceras/sakila

