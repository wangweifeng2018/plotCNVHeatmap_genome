
#改写R 包 copynumber 里面的plotHeatmap函数，实现以下效果
![CNV热图](https://github.com/wangweifeng2018/plotCNVHeatmap_genome/blob/master/CNV_heatmap.png)

#Step1. 下载 Bioconductor-copynumber 源码文件，
```
$wget http://www.bioconductor.org/packages/release/bioc/src/contrib/copynumber_1.26.0.tar.gz
$tar -zxvf copynumber_1.26.0.tar.gz
$cd copynumber/R/
```
#修改addChromlines.r文件在底部添加染色体信息
-----------------
(1)注释掉 row 67,69，改为如下：
```

```
        #Plot half at bottom, half at top:
        #bot <- seq(1,length(chrom.mark),2)
        #top <- seq(2,length(chrom.mark),2)
        #mtext(chrom.names[bot],side=1,line=arg$chrom.line[1],at=at[bot],cex=arg$chrom.cex)
        #mtext(chrom.names,side=1,line=arg$chrom.line[1],at=at[seq(length(chrom.mark))-0.5],cex=arg$chrom.cex)
 ```
        text(x = at[seq(length(chrom.mark))-0.5],y=rep(-3,length(chrom.mark)),labels=chrom.names,pos=1,cex=arg$chrom.cex)
        # added by wangweifeng,at 2019-11-20
        # plot chromosome strip at the bottom of the figure
        xleft <- chrom.mark[1:(length(chrom.mark)-1)]
        xright <- chrom.mark[2:(length(chrom.mark))]
        par(col = "black",bty="n")
        rect(xleft,c(rep(-3,length(chrom.mark)-1)),xright,c(rep(0,length(chrom.mark)-1)),
        col = rep(c("black","white"),length(chrom.mark)-1))
 ```
