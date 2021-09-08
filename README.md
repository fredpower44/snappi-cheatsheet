# snappi-cheatsheet

## snappi Iterators

* Adding item into iterator
    ```
    iter = {iterator}.{item1}().{item2}().{item3}() ...
    ```
    or
    ```
    {iterator}.append({item})
    ```

* Accessing item in iterator
    ```
    item = {iterator}[0]
    ```
    or
    ```
    i1, i2, i3 = {iterator}.{item1}().{item2}().{item3}()
    ```
* Removing item(s) from iterator
    ```
    {iterator}.remove({index})
    ```
    or
    ```
    {iterator}.clear()
    ```