#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Wed Oct  4 10:14:01 2017
DOES THIS COMMENT SHOW UP ON GIT
@author: boughter
"""

import matplotlib.pyplot as mp
import os
import pandas
import glob

os.chdir('/Users/boughter/Desktop/Meredith_group_analysis092017/cntrl')
ff=glob.glob('*.txt')
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

    fig = mp.figure(figsize=(8, 8))
    ax = fig.add_subplot(111)    # The big subplot
    ax1 = fig.add_subplot(211)
    ax2 = fig.add_subplot(212)

    # We need to turn off everything for the big axis (ax)
    ax.spines['top'].set_color('none')
    ax.spines['bottom'].set_color('none')
    ax.spines['left'].set_color('none')
    ax.spines['right'].set_color('none')
    ax.tick_params(labelcolor='w', top='off', bottom='off', left='off', right='off')


    ax1.hist(areaF,bins=100,alpha=0.75,range=(0.00001,max(areaF)),color='black')
    ax1.set_ylim([0,80])
    ax1.set_xlabel('Binned Particle Area [nm^2]',fontsize=16,weight='bold')
    ax.set_ylabel('Number of Particles',fontsize=16,weight='bold')
    ax.set_title(file[:-4]+' Histogram',y=1.08)

    ax2.hist(ZcenF,bins=100,alpha=0.75,range=(0.00001,max(ZcenF)))
    ax2.hist(ZavgF,bins=100,alpha=0.75,range=(0.00001,max(ZavgF)),color='red')
    ax2.set_xlabel('Binned Particle Size [nm]',fontsize=16,weight='bold')
    #ax2.set_ylabel('Number of Particles',fontsize=16,weight='bold')
    #axarr[1].title('Z Histogram')
    ax1.legend(['Area'],fontsize=10)
    ax2.legend(['Center','Average'],fontsize=10)
    
    fig.savefig(file[:-4]+'.pdf')
    fig.clear()
    #axarr.show()
