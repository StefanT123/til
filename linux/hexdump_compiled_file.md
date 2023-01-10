# Hexdump compiled file

The hexdump command allows you to dump the contents of a compiled/executable file in a readable hexadecimal format. Adding the -C flag includes a sidebar with a formatted version of that row of hexadecimal.

The hexdump command can output the contents of a compiled/executable file in a readable hexadecimal format. The key is adding the -C flag. When added it will include a sidebar with a formatted version of that row of hexadecimal.

For example, if we have this Example java class:
```java
class Example {
    public static void main(String[] args) {
        System.out.println("This is an example"); 
    }
}
```
After compiling Example.class will look like this:
```
cafe babe 0000 0037 001d 0a00 0600 0f09
0010 0011 0800 120a 0013 0014 0700 1507
0016 0100 063c 696e 6974 3e01 0003 2829
5601 0004 436f 6465 0100 0f4c 696e 654e
756d 6265 7254 6162 6c65 0100 046d 6169
6e01 0016 285b 4c6a 6176 612f 6c61 6e67
2f53 7472 696e 673b 2956 0100 0a53 6f75
7263 6546 696c 6501 000c 4578 616d 706c
652e 6a61 7661 0c00 0700 0807 0017 0c00
1800 1901 0012 5468 6973 2069 7320 616e
2065 7861 6d70 6c65 0700 1a0c 001b 001c
0100 0745 7861 6d70 6c65 0100 106a 6176
612f 6c61 6e67 2f4f 626a 6563 7401 0010
6a61 7661 2f6c 616e 672f 5379 7374 656d
0100 036f 7574 0100 154c 6a61 7661 2f69
6f2f 5072 696e 7453 7472 6561 6d3b 0100
136a 6176 612f 696f 2f50 7269 6e74 5374
7265 616d 0100 0770 7269 6e74 6c6e 0100
1528 4c6a 6176 612f 6c61 6e67 2f53 7472
696e 673b 2956 0020 0005 0006 0000 0000
0002 0000 0007 0008 0001 0009 0000 001d
0001 0001 0000 0005 2ab7 0001 b100 0000
0100 0a00 0000 0600 0100 0000 0100 0900
0b00 0c00 0100 0900 0000 2500 0200 0100
0000 09b2 0002 1203 b600 04b1 0000 0001
000a 0000 000a 0002 0000 0003 0008 0004
0001 000d 0000 0002 000e
```

If we want to get the compiled contents into somewhat readable format, we are using hexdump:
```bash
cat Example.class | hexdump -C

00000000  ca fe ba be 00 00 00 37  00 1d 0a 00 06 00 0f 09  |.......7........|
00000010  00 10 00 11 08 00 12 0a  00 13 00 14 07 00 15 07  |................|
00000020  00 16 01 00 06 3c 69 6e  69 74 3e 01 00 03 28 29  |.....<init>...()|
00000030  56 01 00 04 43 6f 64 65  01 00 0f 4c 69 6e 65 4e  |V...Code...LineN|
00000040  75 6d 62 65 72 54 61 62  6c 65 01 00 04 6d 61 69  |umberTable...mai|
00000050  6e 01 00 16 28 5b 4c 6a  61 76 61 2f 6c 61 6e 67  |n...([Ljava/lang|
00000060  2f 53 74 72 69 6e 67 3b  29 56 01 00 0a 53 6f 75  |/String;)V...Sou|
00000070  72 63 65 46 69 6c 65 01  00 0c 45 78 61 6d 70 6c  |rceFile...Exampl|
00000080  65 2e 6a 61 76 61 0c 00  07 00 08 07 00 17 0c 00  |e.java..........|
00000090  18 00 19 01 00 12 54 68  69 73 20 69 73 20 61 6e  |......This is an|
000000a0  20 65 78 61 6d 70 6c 65  07 00 1a 0c 00 1b 00 1c  | example........|
000000b0  01 00 07 45 78 61 6d 70  6c 65 01 00 10 6a 61 76  |...Example...jav|
000000c0  61 2f 6c 61 6e 67 2f 4f  62 6a 65 63 74 01 00 10  |a/lang/Object...|
000000d0  6a 61 76 61 2f 6c 61 6e  67 2f 53 79 73 74 65 6d  |java/lang/System|
000000e0  01 00 03 6f 75 74 01 00  15 4c 6a 61 76 61 2f 69  |...out...Ljava/i|
000000f0  6f 2f 50 72 69 6e 74 53  74 72 65 61 6d 3b 01 00  |o/PrintStream;..|
00000100  13 6a 61 76 61 2f 69 6f  2f 50 72 69 6e 74 53 74  |.java/io/PrintSt|
00000110  72 65 61 6d 01 00 07 70  72 69 6e 74 6c 6e 01 00  |ream...println..|
00000120  15 28 4c 6a 61 76 61 2f  6c 61 6e 67 2f 53 74 72  |.(Ljava/lang/Str|
00000130  69 6e 67 3b 29 56 00 20  00 05 00 06 00 00 00 00  |ing;)V. ........|
00000140  00 02 00 00 00 07 00 08  00 01 00 09 00 00 00 1d  |................|
00000150  00 01 00 01 00 00 00 05  2a b7 00 01 b1 00 00 00  |........*.......|
00000160  01 00 0a 00 00 00 06 00  01 00 00 00 01 00 09 00  |................|
00000170  0b 00 0c 00 01 00 09 00  00 00 25 00 02 00 01 00  |..........%.....|
00000180  00 00 09 b2 00 02 12 03  b6 00 04 b1 00 00 00 01  |................|
00000190  00 0a 00 00 00 0a 00 02  00 00 00 03 00 08 00 04  |................|
000001a0  00 01 00 0d 00 00 00 02  00 0e                    |..........|
000001aa
```