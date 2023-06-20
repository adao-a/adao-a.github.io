---
title: 【Algorithms Part Ⅰ】lab1 percolation
date: 2023-03-18 22:57:49
---

并查集的简单应用，模拟解决渗透（percolation）问题
<!--more-->

# **The model**：

- We model a percolation system using an **n-by-n grid of sites**. Each site is either open or blocked. 
- A full site is an open site that can be connected to an open site in the top row via a chain of neighboring (left, right, up, down) open sites. 
- We say the system percolates if there is a full site in the bottom row. In other words, a system percolates if we fill all open sites connected to the top row and that process fills some open site on the bottom row.

<p align="center">
<img src="https://tzuming-blog-1313166118.cos.ap-guangzhou.myqcloud.com/percolates-no.png" width="400" />
<img src="https://tzuming-blog-1313166118.cos.ap-guangzhou.myqcloud.com/percolates-yes.png" width="400" />
</p>




# The problem:

When n is sufficiently large, there is a **threshold value p*** such that when p < p* a random n-by-n grid almost never percolates, and when p > p*, a random n-by-n grid almost always percolates. No mathematical solution for determining the percolation threshold p* has yet been derived. Your task is to **write a computer program to estimate p*.**
<p align="center">
<img src="https://tzuming-blog-1313166118.cos.ap-guangzhou.myqcloud.com/percolation-threshold20.png" width="400" />
</p>



# Solution:

分两部分，第一部分建立模型，以及实现并查集相关操作。第二部分计算出p*

## 模型

```java
public class Percolation { 
	// creates n-by-n grid, with all sites initially blocked 
    public Percolation(int n) 
        
    // opens the site (row, col) if it is not open already 
	public void open(int row, int col) 
        
    // is the site (row, col) open? 
    public boolean isOpen(int row, int col) 
        
    // is the site (row, col) full?
    public boolean isFull(int row, int col) 
        
    // returns the number of open sites 
    public int numberOfOpenSites() 
        
    // does the system percolate? 
    public boolean percolates() 
        
    // test client (optional) 
    public static void main(String[] args) }
```



- 建立一维数组，用row,col即可定位

- 一个个检查第一行和最后一行的方块有点麻烦，可以假装上下各有一个方块，上面的和第一行全部方块都相连，下面类似。那么只要判断这两个虚拟方块是否连通即可，连通则系统可以渗透。

  <img src="https://tzuming-blog-1313166118.cos.ap-guangzhou.myqcloud.com/virtual-site.png" width="400" />

## 计算

重复这个计算实验 T 次取平均值,方差,置信区间

```java
public class PercolationStats { 
	// perform independent trials on an n-by-n grid 
    public PercolationStats(int n, int trials) 
        
    // sample mean of percolation threshold 
    public double mean()
        
    // sample standard deviation of percolation threshold 
    public double stddev()
        
    // low endpoint of 95% confidence interval 
    public double confidenceLo() 
        
    // high endpoint of 95% confidence interval 
    public double confidenceHi() 
        
    // test client (see below) 
    public static void main(String[] args) 
        
}
```