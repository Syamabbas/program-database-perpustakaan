# Library Database Program with Python

## Problem Statement: 
A library wants to create a database system to manage their collection of books. They want to create a program that allows them to add, update, and delete books in their collection.

## Solution:
We can use Python programming language to create a CRUD system for the library's database. The CRUD system will allow the librarian to perform the following operations:
 - Create: Add new books to the library's collection.
 - Read: Display the books in the library's collection. 
 - Update: Modify the details of a book in the library's collection.
 - Delete: Remove a book from the library's collection.
 
## Implementation
1.  **Preparing a file:** The first step is to create a database to store the library's collection of books. We can use input function to adding new data into database. We can create also database called `database.py` and to create new database with `.txt` file we can write this code:

```sh
DB_NAME = "data.txt"
TEMPLATE = {
    "pk":"XXXXXX",
    "date_add":"yyyy-mm-dd",
    "judul":255*" ",
    "penulis":255*" ",
    "tahun":"yyyy"
}
```

Beside of that we make `main.py` that include main of code such as CRUD function, beginning of program and ending of program. We also make `view.py` that include code used for viewer.

CRUD function that include in `main.py` :
```
match user_option:
   case "1": CRUD.read_console()
   case "2": CRUD.create_console()
   case "3": CRUD.update_console()
   case "4": CRUD.delete_console()
```

2.  **Adding a book to the database:** We can add or create a new book to the database using the `create.console()` with this code:

```
def create_console():
    print("\n\n"+"="*100)
    print("Silahkan tambah data buku\n")
    penulis = input("Penulis\t: ")
    judul = input("Judul\t: ")
    while(True):
        try:
            tahun = int(input("Tahun\t: "))
            if len(str(tahun)) == 4:
                break
            else:
                print("tahun harus angka, silahkan masukan tahun lagi (yyyy)")    
        except:
            print("tahun harus angka, silahkan masukan tahun lagi (yyyy)")
    Operasi.create(tahun,judul,penulis)
    print("\nBerikut adalah data baru anda")
    read_console()
```

3.  **Displaying the Books in database:** We can display all the books in the database using the `read.console` Here's a code:

```
def read_console():
    data_file = Operasi.read()
    
    index = "No"
    judul = "Judul"
    penulis = "Penulis"
    tahun = "Tahun"
```

4.  **Updating a database:** We can update the details of a book in the database using the `update.console` with this code:

```
def update_console():
    read_console()
    while(True):
        print("Silahkan pilih nomor buku yang akan di update")
        no_buku = int(input("Nomor Buku: "))
        data_buku = Operasi.read(index=no_buku)

        if data_buku:
            break
        else:
            print("nomor tidak valid, silahkan masukan lagi")
    
    data_break = data_buku.split(',')
    pk = data_break[0]
    data_add = data_break[1]
    penulis = data_break[2]
    judul = data_break[3]
    tahun = data_break[4][:-1]
    
    while(True):
        # data yang ingin diupdate
        print("\n"+"="*100)
        print("Silahkan pilih data apa yang ingin anda ubah")
        print(f"1. Judul\t: {judul:.40}")
        print(f"2. Penulis\t: {penulis:.40}")
        print(f"3. Tahun\t: {tahun:4}")

        # memilih mode untuk update
        user_option = input("Pilih data [1,2,3]: ")
        print("\n"+"="*100)
        match user_option:
            case "1": judul = input("judul\t: ")
            case "2": penulis = input("penulis\t: ")
            case "3": 
                while(True):
                    try:
                        tahun = int(input("Tahun\t: "))
                        if len(str(tahun)) == 4:
                            break
                        else:
                            print("tahun harus angka, silahkan masukan tahun lagi (yyyy)")    
                    except:
                        print("tahun harus angka, silahkan masukan tahun lagi (yyyy)")
                        case _: print("index tidak cuocuoook")

        print("Data baru anda")
        print(f"1. Judul\t: {judul:.40}")
        print(f"2. Penulis\t: {penulis:.40}")
        print(f"3. Tahun\t: {tahun:4}")
        is_done = input("Apakah data sudah sesuai(y/n)? ")
        if is_done == "y" or is_done == "Y":
            break
    
    Operasi.update(no_buku,pk,data_add,tahun,judul,penulis)
```

5.  **Deleting a book from database:** We can delete a book from the database using the `delete.console` . Here's an example:

```
def delete(no_buku):
    try:
        with open(Database.DB_NAME,'r') as file:
            counter = 0

            while(True):
                content = file.readline()
                if len(content) == 0:
                    break
                elif counter == no_buku - 1:
                    pass
                else:
                    with open("data_temp.txt",'a',encoding="utf-8") as temp_file:
                        temp_file.write(content)
                counter += 1
    except:
        print("database error")
    
    os.rename("data_temp.txt",Database.DB_NAME)
```


*Click this link to see complete code*
