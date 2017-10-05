#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Wed Oct  4 10:14:01 2017

@author: boughter
"""

import numpy as np
import matplotlib.pyplot as mp
import matplotlib.mlab as mlab
import os
import pandas
import glob

os.chdir('/Users/boughter/Desktop/Meredith_group_analysis092017/')
#ff=glob.glob('*0002*.txt')
ff=['200um/ab40_200um0002_2nm.txt','20um/ab40_20um_flush0007_2nm.txt','cntrl/blank_take2_wait0002_2nm.txt']
#ff=['ab40_20um_flush0007_1nm.txt','ab40_20um_set20002_1nm.txt']
fig= mp.figure(figsize=(8, 6))
for i in ff:
    file=i
    #x=np.loadtxt(file)
    x=pandas.read_csv(file)
    mapp=x.as_matrix()

    # Initialize all the stuff we're pulling out.
    Zcen=[] # 1st column
    Zavg=[] # 2nd column
    area=[] # 3rd column

    for i in range(len(mapp)):
        start=str(mapp[i])
        l1=start.find('\\t')
        l2=start[l1+2:].find('\\t')+l1+2
        l3=start[l2+2:].find('\\t')+l2+2
        Zcen=Zcen+[start[3:l1]]
        Zavg=Zavg+[start[l1+2:l2]]
        area=area+[start[l2+2:l3]]

    # Need to fill in any blank spots with a 0
    a=0
    for i in Zcen:
        if i=='':
            Zcen[a]='0'
        a=a+1
    a=0
    for i in Zavg:
        if i=='':
            Zavg[a]='0'
        a=a+1
    a=0
    for i in area:
        if i=='':
            area[a]='0'
        a=a+1
        # Cool now we have all our data, take the float of it.
    ZcenF=[float(z)*10**9 for z in Zcen]
    ZavgF=[float(z)*10**9 for z in Zavg]
    areaF=[float(z)*10**18 for z in area]

    #plot each one of these:

   # fig= mp.figure(figsize=(8, 8))
    ax = fig.add_subplot(111)    # The big subplot
    
    fig.suptitle('Histogram - Compare Zooms')
    
    #### This bit is for comparing multiple plots to one figure
    ax.hist(ZavgF,bins=np.arange(0.5,12,0.1),alpha=0.75,range=(0.00001,max(ZavgF)))
    ax.set_xlabel('Binned Particle Size [nm]',fontsize=16,weight='bold')
    ax.set_ylabel('Number of Particles',fontsize=16,weight='bold')
    ax.legend(['200 uM','20 uM','Control'],fontsize=14)
    fig.savefig('compare_concentrations_2nm.pdf')
    #axarr.show()
