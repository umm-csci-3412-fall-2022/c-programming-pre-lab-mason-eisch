# Leak report
strip() result 

The result of strip is allocated memory that is never freed. In order to handle this, I added free statements to the tests that invoke it. Additionally, the result of strip() when called in check\_clean() wasn't being properly dealt with. At first I just tried to free the pointer cleaned which referenced the result of strip(), but this was causing issues when checkstrip was called on a blank string because strip() doesn't actually bother allocating memory in such a case and just returns an empty string. To deal with this, I added an if statement to the end of check\_clean() that makes sure that cleaned actually has stuff in it. Once I had dealt with this edge case, valgrind was finally happy :D 
