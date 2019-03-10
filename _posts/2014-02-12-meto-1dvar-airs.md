---
id: 260
title: meto_1dvarでAIRSのリトリーバル
date: 2014-02-12T07:31:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2014/02/12/meto-1dvar-airs/
permalink: /2014/02/12/meto-1dvar-airs/
tumblr_hiyokoz_permalink:
  - http://hiyokoz.tumblr.com/post/76409012738/meto-1dvar-airs
tumblr_hiyokoz_id:
  - "76409012738"
categories:
  - 研究
tags:
  - AIRS
  - retrieval
---
今度はAIRSのサンプルを動かしてみる。
<!--more-->

test.shにもう少し汎用性を持たせてみる。
<pre><code>SATELLITE=EOS
INSTRUMENT=AIRS

satellite=`echo ${SATELLITE} | tr A-Z a-z`
instrument=`echo ${INSTRUMENT} | tr A-Z a-z`

LEVELS=51

BGDIR=../../Sample_Background
NLDIR=../../Sample_Namelists
OBDIR=../../Sample_ObsFiles
COEFDIR=../${INSTRUMENT}_COEFFS_DIR
RUNDIR=../test/${instrument}
BINDIR=../../src

COEFFILE=rtcoef_${satellite}_2_${instrument}.dat
if [ ! -f ${COEFDIR}/${COEFFILE} ]; then
  echo "Download ${COEFFILE}, extract and place in ${COEFDIR}."
  exit
fi

if [ -d ${RUNDIR} ]; then
  rm -rf ${RUNDIR}
fi
mkdir -p ${RUNDIR}/${INSTRUMENT}_COEFFS_DIR

cd ${RUNDIR}
if [ ${LEVELS} -eq 51 ]; then
  LEV=_${LEVELS}L
else
  LEV=""
fi
ln -s ${BGDIR}/BACKGROUND_MidLatWin${LEV}.dat BACKGROUND.dat 
ln -s ${NLDIR}/Retrieval_${INSTRUMENT}${LEV}.NL Retrieval.NL
cp ../../${INSTRUMENT}_COEFFS_DIR/Bmatrix_${LEVELS}L ${INSTRUMENT}_COEFFS_DIR/Bmatrix
cp ../${COEFDIR}/Rmatrix ${INSTRUMENT}_COEFFS_DIR
cp ../${COEFDIR}/ChannelChoice.dat ${INSTRUMENT}_COEFFS_DIR
ln -s ../${COEFDIR}/${COEFFILE} .
ln -s ${BINDIR}/IASI_1DVar ${INSTRUMENT}_1DVar
ln -s ${NLDIR}/ControlData_${INSTRUMENT}.NL ControlData.NL
ln -s ${OBDIR}/ObsFile_${INSTRUMENT}.dat ObsFile.dat

echo "Run ${INSTRUMENT}_1DVar in ${RUNDIR}"
</code></pre>