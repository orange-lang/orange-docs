# Source Format 

Orange source code files are compiled with UTF-8. All of the keywords defined for Orange use standard ASCII characters, but function names, strings, and variables all support Unicode.

The compiler ignores most whitespace, with the exception of newlines. Lines of code are separated by newlines or semicolons. Multiple empty lines are ignored. 

Comments in Orange start with `#`. Once the compiler sees a `#`, the rest of the line is ignored. There is no current support for multiline comments.

Here is an exhaustive list of all keywords defined in Orange, whether or not they are currently in use:

1. false
2. true
3. def
4. return
5. if
6. elif
7. else
8. end
9. for
10. forever
11. loop
12. continue
13. break
14. do
15. while
16. when
17. unless
18. class
19. using
20. public
21. private
22. package
23. export
24. extern
25. shared
26. const
27. char
28. int
29. uint
30. float
31. double
32. int8
33. uint8
34. int16
35. uint16
36. int32
37. uint32
38. int64
39. uint64
40. id
41. var 
