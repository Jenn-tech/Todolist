# 목차

- [목차](#목차)
- [1. Adding Entries](#1-adding-entries)
- [2. Deleting Entries](#2-deleting-entries)
- [3. Done Marking](#3-done-marking)
- [4. Category](#4-category)
- [5. Filter by category](#5-filter-by-category)
- [6. Auto-update Options](#6-auto-update-options)
- [7. localStorage](#7-localstorage)

# 1. Adding Entries
- change Event Listener
- innerHTML +=
- createElement
- appendChild

# 2. Deleting Entries
- doubleclick event
- remove()
- Material Icons
  - ref : https://material.io/
- className
- Closures

# 3. Done Marking
- text-decoration : line-through;
- JS technique : flag
- js classList API(strike)

```javascript
  
        function done(){
            if(flag){
              //this.style.textDecoration = "line-through";
              this.classList.add("strike");
              flag = !flag;
            }else{
              //this.style.textDecoration = "none";
              this.classList.remove("strike");
              flag = !flag;
            }
            
          }
```

- HTML `input` checkbox
- CSS : checked
```css
input:checked + span{
    text-decoration: line-through;
}
```
- CSS ~ and +

# 4. Category
- getElementById
- new row in table
```javascript
        //add a new row
         
        let table = document.getElementById("todoTable");

        let trElem = document.createElement("tr");
        table.appendChild(trElem);

        //checkbox cell
        let checkboxElem = document.createElement("input");
        checkboxElem.type= "checkbox";
        checkboxElem.addEventListener("click", done, false);
        let tdElem1 = document.createElement("td");
        tdElem1.appendChild(checkboxElem);
        trElem.appendChild(tdElem1);

        //to-do list cell
        let tdElem2 = document.createElement("td");
        tdElem2.innerText = inputValue;
        trElem.appendChild(tdElem2);

        //category cell
        let tdElem3 = document.createElement("td");
        tdElem3.innerText = inputValue2;
        trElem.appendChild(tdElem3);

        //delete cell
        let spanElem = document.createElement("span");
        spanElem.innerText = "remove_circle_outline";
        spanElem.className = "material-icons";
        spanElem.addEventListener("click", deleteItem, false);
        let tdElem4 = document.createElement("td");
        tdElem4.appendChild(spanElem);
        trElem.appendChild(tdElem4);
```
- classList.toggle()
```javascript
checkboxElem.addEventListener("click", done, false);
        function done(){
           trElem.classList.toggle("strike");
          }
```
- datalist
```html
 <p><input type = "text" placeholder="카테고리 입력" list ="categoryList"><p>
    <datalist id = "categoryList">
        <option value="Personal"></option>
        <option value="work"></option>
    </datalist>
```


# 5. Filter by category
- `<select>`
```html
                <select id="categoryFilter">
                    <option value = "Personal">Personal</option>
                    <option value = "Work">Work</option>
                </select>
```
- Element.style.display
```javascript
       function filterEntries(){
            let rows = document.getElementsByTagName("tr");
            
            for (let i = 1; i <rows.length; i++){
                let category = rows[i].getElementsByTagName("td")[2].innerText;
                if(category == selectElem.value ){
                    rows[i].style.display = "";
                }else{
                    rows[i].style.display = "none";
                }


            }
            
            
        }
```
- Es6 Array.from()
- Es6 Array.prototype.forEach()
```javascript
        function filterEntries(){
            let selection = selectElem.value;

            if(selection =="total"){
                
                let rows = document.getElementsByTagName("tr");
                
                Array.from(rows).forEach((row, index)=>{
                   
                 row.style.display = "";
                           
                });
            }else{

                let rows = document.getElementsByTagName("tr");
                
                Array.from(rows).forEach((row, index)=>{
                    if(index==0){
                        return;
                    }
                    let category = row.getElementsByTagName("td")[2].innerText;
                    if(category == selectElem.value ){
                                row.style.display = "";
                            }else{
                                row.style.display = "none";
                            }
                });
            }
        }
```

# 6. Auto-update Options
- add option
```javascript
let newOptionElem = document.createElement('option');
                newOptionElem.value = option;
                newOptionElem.innerText= option;
                selectElem.appendChild(newOptionElem);
```
- Array push()
- Array incudes()
  - if you add a category with the same name as it was originally
```javascript
  if(!options.includes(category)){
                options.push(category);

            }
```

- new Set()
  - not allows duplicate 
  - faster than using includes (running just one)
```javascript
    let optionSet = new Set(options);
```
- for of loop
```javascript
            for(let option of optionSet){

                let newOptionElem = document.createElement('option');
                newOptionElem.value = option;
                newOptionElem.innerText= option;
                selectElem.appendChild(newOptionElem);
        
            }
```
- const
```javascript
    const DEFAULT_OPTION = "Category"; 

```

# 7. localStorage
- localStorage.setItem()
```javascript
    function save(){
        localStorage.setItem("todoList", todoList);
    }
```
- localStorage.getItem()
- JSON.stringify()
```javascript
   function save(){
        let stringified = JSON.stringify(todoList);
        localStorage.setItem("todoList", stringified);
    }

    function load(){
        
        todoList = localStorage.getItem("todoList");
        console.log(typeof todoList);
        if(todoList ==null)
            todoList = [];
    
    }
```
- JSON.parse()
```javascript

    function load(){
        
        let retrieved = localStorage.getItem("todoList");
        todoList = JSON.parse(retrieved);
        console.log(typeof todoList);
        if(todoList ==null)
            todoList = [];
    
    }
```