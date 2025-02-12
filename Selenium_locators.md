https://www.cricbuzz.com/### 
1)  **Single slash vs double slash**  
       **A. Single slash**  
        - **Absolute XPath**  
        - **Fixed path from root**  
        ```java
        /html/body/div/input
        ```  
     **B. Double slash**  
        - **Relative XPath**  
        - **Searches anywhere**  
        ```java
        //input[@id='username']
        ```  

###  2)  **Id**  
   **A. XPath**  
        ```java
        //*[@id="teamDropDown"]
        ```  
     **B. CSS Selectors**  
        ```java
        div[id="teamDropDown"]
        ```  

###  3)  **XPath Using Text Matching**  
   **A. Contains**  
        ```java
        //a[contains(text(),'Rankings')]
        ```  
     **B. starts-with**  
        ```java
        //div[starts-with(@class,'alert')]
        ```  

###  4)  **Sibling**  
   **A. following-sibling**  
        - **Selects only sibling elements (elements that share the same parent) that appear after the current node.**  
        - **It does not select elements outside of the same parent.**  
        ```java
        //*[@id="teamDropDown"]/following-sibling::div
        ```  
     **B. preceding-sibling**  
        ```java
        //*[@id="teamDropDown"]/preceding-sibling::div
        ```  
     **C. following**  
        - **Selects all elements that appear after the current node in the document, regardless of their hierarchy (not limited to siblings).**  
        - **Can select descendants, siblings, and other elements that come later in the DOM.**  
        ```java
        //*[@id="teamDropDown"]/following::div
        ```  
     **D. preceding**  
        ```java
        //*[@id="teamDropDown"]/preceding::div
        ```  

###  5)  **XPath Using parent and ancestor**  
   **A. Parent**  
        ```java
        //*[@id="teamDropDown"]/parent::nav
        ```  
     **B. Ancestor**  
        ```java
        //*[@id="teamDropDown"]/ancestor::div
        ```  

###  6)  **AND OR**  
   **A. AND**  
        ```java
        //*[@id="teamDropDown" and @title='Cricket Teams']
        ```  
     **B. OR**  
        ```java
        //*[@id="teamDropDown" or @title='Cricket Teams']
        ```  
