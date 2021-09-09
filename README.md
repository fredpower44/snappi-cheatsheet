# snappi-cheatsheet

## snappi Iterators

snappi iterators are used to represent lists of snappi objects. They can be used similarly to lists in Python.

* Adding item into iterator
    ```
    iter = {iterator}.{item1}().{item2}().{item3}() ...
    ```
    * <details>
        <summary>example: </summary>
        
        ```
        port_iter = cfg.ports.port(name='p1').port(name='p2').port(name='p3')
        ```
        </details>
    or
    ```
    {iterator}.append({item}) 
    ```
    * <details>
        <summary>example: </summary>
        
        ```
        f = snappi.Flow(name='f')
        cfg.flows.append(f)
        ```
        </details>

* Accessing item in iterator
    ```
    item = {iterator}[0]
    ```
    * <details>
        <summary>example: </summary>
        
        ```
        port0 = cfg.ports[0]
        ```
        example 2:
        ```
        port2 = cfg.ports.port(name='p0').port(name='p1').port(name='p2')[-1]
        ```
        </details>
    or
    ```
    i1, i2, i3 = {iterator}.{item1}().{item2}().{item3}() # Declares and accesses in same line
    ```
    * <details>
        <summary>example: </summary>
        
        ```
        f1, f2, f3 = cfg.flows.flow(name='f1').flow(name='f2').flow(name='f3')
        ```
        </details>

* Removing item(s) from iterator
    ```
    {iterator}.remove({index}) # Removes object at iterator's index
    ```
    * <details>
        <summary>example: </summary>
        
        ```
        cfg.flows.flow(name='f1').flow(name='f2').flow(name='f3')
        cfg.flows.remove(1)
        ```
        </details>
    or
    ```
    {iterator}.clear() # Clears the iterator
    ```
    * <details>
        <summary>example: </summary>
        
        ```
        cfg.ports.port(name='p1').port(name='p2').port(name='p3')
        cfg.ports.clear()
        ```
        </details>