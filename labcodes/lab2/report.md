##练习1##

###实现 first-fit 连续物理内存分配算法###

注意在freelist中，按物理地址从低到高排序。

###请描述页目录项(Pag Director Entry)和页表(Page Table Entry)中每个组成部分的含义和以及对ucore而言的潜在用处###

线性地址的结构：

// +--------10------+-------10-------+---------12----------+
// | Page Directory |   Page Table   | Offset within Page  |
// |      Index     |     Index      |                     |
// +----------------+----------------+---------------------+
//  \--- PDX(la) --/ \--- PTX(la) --/ \---- PGOFF(la) ----/
//  \----------- PPN(la) -----------/

而PDE和PTE不需要offset，而最后12位保存的是权限位，最大是 0xE00。

###如果ucore执行过程中访问内存,出现了页访问异常,请问硬件要做哪些事情?###

会调用缺页中断处理异常。

###数据结构Page的全局变量(其实是一个数组)的每一项与页表中的页目录项和页表项有无对应关系?如果有,其对应关系是啥?###

有，`physical_address == &pages[PPN(pa)]`, `physical_address == virtual_address - KERNBASE`
