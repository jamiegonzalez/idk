- [Binlister Cheat Sheet](#binlister-cheat-sheet)
- [Tutorial: Binlister Demo 1](#tutorial-binlister-demo-1)
- [Tutorial: Binlister Demo 2](#tutorial-binlister-demo-2)
- [Tutorial: Binlister Demo 3](#tutorial-binlister-demo-3)
- [Tutorial: Binlister Demo 4](#tutorial-binlister-demo-4)

## Binlister Cheat Sheet

Operator |	Format | Example
----- | ----- | -----
 Home-item operator	| .|	.{11}
 NOT operator|	  ~|	 .{~11}
 Event-list operator|	 {event_#}|	 .{11}
 OR operator|	 ; or ,|	 .{11;22;33} or .{11,22,33}
Colon operator|	: or -|	.{10:20} or .{10-20}
 Reaction-time operator|	 :rt<“variable_name”>|	 .{11}{9:rt<“correct_resp”>}
 Time-condition operator|	 t<start_#_ms - stop_#_ms>|	 .{11}{t<100-1000>9}
 Flag operator-Write artifact flag| :wa<binary_#>|	 .{11:wa<000000001>}
 Flag operator-Test artifact flag| 	 :fa<binary_#>|	.{11:fa<000000001>}
 Flag operator-Write user flag|	 :wb<binary_#>|	 .{11:wb<10000000>}
 Flag operator-Test user flag|	 :fb<binary_#>|	.{11:wb<10000000>}
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>


## Tutorial: Binlister Demo 1
```
bin 1
Frequent followed by correct response
.{11;122;22;111}{9}

bin 2
Rare followed by correct response
.{21;112;12;121}{9}
```

----
See also:
- [Tutorial: Binlister Demo 1](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-1)
- [Tutorial: Binlister Demo 2](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-2)
- [Tutorial: Binlister Demo 3](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-3)
- [Tutorial: Binlister Demo 4](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-4)
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

## Tutorial: Binlister Demo 2
```
bin 1
Frequent followed by correct response
.{11;122;22;111}{9}

bin 2
Rare followed by correct response
.{21;112;12;121}{9}
```

----
See also:
- [Tutorial: Binlister Demo 1](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-1)
- [Tutorial: Binlister Demo 2](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-2)
- [Tutorial: Binlister Demo 3](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-3)
- [Tutorial: Binlister Demo 4](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-4)
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

## Tutorial: Binlister Demo 3
```
bin 1
Frequent followed by correct response without incorrect response
.{11;122;22;111}{t<200-1000>~8}{t<200-1000>9}

bin 2
Rare followed by correct response without incorrect response
.{21;112;12;121}{t<200-1000>~8}{t<200-1000>9}
```

----
See also:
- [Tutorial: Binlister Demo 1](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-1)
- [Tutorial: Binlister Demo 2](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-2)
- [Tutorial: Binlister Demo 3](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-3)
- [Tutorial: Binlister Demo 4](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-4)
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

## Tutorial: Binlister Demo 4
```
bin 1
Frequent followed by correct response without incorrect response
.{11;122;22;111}{t<200-1000>~8}{t<200-1000>9:rt<"Frequent RT">}

bin 2
Rare followed by correct response without incorrect response
.{21;112;12;121}{t<200-1000>~8}{t<200-1000>9:rt<"Rare RT">}
```

Exclude double responses. The bin descriptors look for a stimulus (e.g. 11;122;22;111) that is not followed by the event code 8 between 200-1000 ms and is followed by the event code 9 between 200-1000 ms.

----
See also:
- [Tutorial: Binlister Demo 1](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-1)
- [Tutorial: Binlister Demo 2](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-2)
- [Tutorial: Binlister Demo 3](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-3)
- [Tutorial: Binlister Demo 4](https://github.com/lucklab/erplab/wiki/_new#tutorial-binlister-demo-4)
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>