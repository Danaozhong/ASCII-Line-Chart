# ASCII-Line-Chart
A C++ library to draw ASCII graphs, line charts, e.g. to print them out on the console or UART.


# How to use it?

You first need to instantiate a ASCIIGraphNs::DataTable object, and fill it with the data points you want to display. You can simply pass a std::vector<std::pair<int32_t, int32_t>> to the constructor.

The first entry is the x value, the second y. 
```cpp
const ASCIIGraphNs::DataTable<int32_t, int32_t> data = std::vector<std::pair<int32_t, int32_t>> {
    std::pair<int32_t, int32_t>(0, 0),
    std::pair<int32_t, int32_t>(10, 20),
    std::pair<int32_t, int32_t>(50, 50),
    std::pair<int32_t, int32_t>(100, 0)
};
```

To display a table, you then need to crease an ASCIIGraphNs::ASCIIGraph object. In the constructor,
you provide certain settings to describe the size of the chart.

```cpp
ASCIIGraphNs::ASCIIGraph o_ascii_diagram(80, 70, 40);
```
The first parameter is the line length, this is usually 80 characters. The second parameter is the width of the chart, the third the height of the chart.

Finally, you can display the chart using these commands below:
```cpp
const size_t buffer_size = 500u;
char output_buffer[buffer_size];
o_ascii_diagram.draw(data, output_buffer, buffer_size);
```

It is even possible to use smaller buffers than what would be needed; and render the diagram in several
small steps. The code documentation provides a method on how to do this.

# How does it look like?


This is an example on how a chart looks like when printed:
```cpp
      4828A│    └┐                                                              
          ││     └─┐                                                            
          ││       └─┐                                                          
          ││         └──┐                                                       
          ││            └───┐                                                   
          ││                └──┐                                                
      3796┤│                   └─┐                                              
          ││                     └──┐                                           
          ││                        └──┐                                        
          ││                           └─┐                                      
          ││                             └─┐                                    
          │┘                               └─┐                                  
      2764┤                                  └─┐                                
          │                                    └─┐                              
          │                                      └─┐                            
          │                                        └─┐                          
          │                                          └──┐                       
          │                                             └─┐                     
      1732┤                                               └──┐                  
          │                                                  └─┐                
          │                                                    └──┐             
          │                                                       └─┐           
          │                                                         └─┐         
          │                                                           └─┐       
       700└────────────────┬────────────────┬────────────────┬────────────────┬>
        -1000            1956             4913             7869             10826
```

# How to Integrate?
The library is basicially just two files. Just include them in your project, or integrate the CMake file, such as:
```cmake
add_subdirectory(ascii_graph)
target_link_libraries(${CMAKE_PROJECT_NAME} ascii_graph)
```
The library is currently in a very early stage of development. There might be small issues left.

