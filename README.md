# CS50's Introduction to Computer Science
## HarvardX - CS50x
### Week 5 Problem Set - Recover
<hr>


### Assignment and Requirements:
Write and execute a progragram that iterates over .raw files, looking for JPEG signatures and recovers images from memory card.

**JPEG Signatures**

JPEGs have “signatures,” patterns of bytes that can distinguish them from other file formats. Specifically, the first three bytes of JPEGs are
```
0xff 0xd8 0xff
```
from first byte to third byte, left to right. 
The fourth byte is either ```0xe0, 0xe1, 0xe2, 0xe3, 0xe4, 0xe5, 0xe6, 0xe7, 0xe8, 0xe9, 0xea, 0xeb, 0xec, 0xed, 0xee, or 0xef```. Hence, the fourth byte’s first four bits are 1110. If this pattern of four bytes can be find on media, images can be restored.

```C
while (fread(&buffer, 512, 1, file_pointer) == 1)
        {

            if (buffer[0] == 0xff && buffer[1] == 0xd8 && buffer[2] == 0xff && (buffer[3] & 0xf0) == 0xe0)
            {
                if (!(count == 0))
                {
                    fclose(img_pointer);
                }

                sprintf(filename, "%03i.jpg", count);
                img_pointer = fopen(filename, "w");
                count++;
            }

            if (!(count == 0))
            {
                fwrite(&buffer, 512, 1, img_pointer);
            }
        }
```

#### Compiling And Execution:

Before execution of the program, it must be compiled with a compiler, translating it from source code into machine code.\
Execute the command below in the Command Line to do that:

```
make recover
```

Execute the program by executing the below:
```
./recover IMAGE
```
where ```IMAGE``` is the name of the forensic image.
