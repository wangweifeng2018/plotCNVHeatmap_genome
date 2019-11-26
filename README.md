
#改写R 包 copynumber 里面的plotHeatmap函数，实现以下效果
![CNV热图](https://github.com/wangweifeng2018/plotCNVHeatmap_genome/blob/master/CNV_heatmap.png)
<img src="https://github.com/wangweifeng2018/plotCNVHeatmap_genome/blob/master/CNV_heatmap.png" width="250" height="250" alt="CNV热图"/>
#Step1. 下载 Bioconductor-copynumber 源码文件
```
$wget http://www.bioconductor.org/packages/release/bioc/src/contrib/copynumber_1.26.0.tar.gz
$tar -zxvf copynumber_1.26.0.tar.gz
$cd copynumber/
```
#修改addChromlines.r文件在底部添加染色体信息
-----------------
        # changed by wangweifeng,at 2019-11-22, give chrom.name at 47,53 line
        #chrom.names <- unique(chromosomes)
        #Plot half at bottom, half at top:
        #bot <- seq(1,length(chrom.mark),2)
        #top <- seq(2,length(chrom.mark),2)
        #mtext(chrom.names[bot],side=1,line=arg$chrom.line[1],at=at[bot],cex=arg$chrom.cex)
        #mtext(chrom.names[top],side=3,line=arg$chrom.line[2],at=at[top],cex=arg$chrom.cex)
        ## changed by wangweifeng , at 2019-11-20. conver 23 to X, 24 to Y
        #mtext(chrom.names,side=1,line=arg$chrom.line[1],at=at[seq(length(chrom.mark))-0.5],cex=arg$chrom.cex)
        text(x = at[seq(length(chrom.mark))-0.5],y=rep(-3,length(chrom.mark)),labels=chrom.names,pos=1,cex=arg$chrom.cex)
        # added by wangweifeng,at 2019-11-20
        # plot chromosome strip at the bottom of the figure
        xleft <- chrom.mark[1:(length(chrom.mark)-1)]
        xright <- chrom.mark[2:(length(chrom.mark))]
        par(col = "black",bty="n")
        rect(xleft,c(rep(-3,length(chrom.mark)-1)),xright,c(rep(0,length(chrom.mark)-1)),
        col = rep(c("black","white"),length(chrom.mark)-1))
