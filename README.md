# 목차

- [목차](#목차)
- [1. Adding Entries](#1-adding-entries)
- [2. Deleting Entries](#2-deleting-entries)
- [3. Done Marking](#3-done-marking)
- [4. Category](#4-category)

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