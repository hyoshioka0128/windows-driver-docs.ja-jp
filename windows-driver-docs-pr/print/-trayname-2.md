---
title: '\ TrayName\ (OutputBins)'
description: '\ TrayName\ (OutputBins)'
ms.assetid: efdb5ecb-3abc-4dfd-8087-7f4f3a938cf2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6343d495b0ed5f5b2803f6a81c61ed1c2b5240d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372886"
---
# <a name="trayname-outputbins"></a>\[TrayName\] (OutputBins)


スキーマのパス:\\Printer.Finishing.OutputBins\[ 。TrayName\]

ノード型: プロパティ

説明: に IHV マップのプロパティ名、出力トレイをします。 IHV は、次の一覧から名前で、出力トレイの IHV 固有トレイ名にマップできます。

OutputBin1

OutputBin2

OutputBin*xx* (*xx*正の整数)

TopBin

MiddleBin

BottomBin

LargeCapacityBin

FaceUpBin

FaceDownBin

MailboxBin

\[TrayName\]プロパティには、次の 3 つの子の値が含まれています。インストールされている、容量、およびレベル。

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> インストールされています。

スキーマのパス:\\Printer.Finishing.OutputBins\[ 。TrayName\]: インストールされています。

ノード型: 値

データ型: BIDI\_BOOL

説明: ビンがによって参照されるかどうかを判断します\[TrayName\]デバイスにインストールされます。 場合**TRUE**、;、デバイスでそのビンがインストールされている場合は**FALSE**、そのビンがデバイスにインストールされていません。

### <a name="span-idcapacityspanspan-idcapacityspan-capacity"></a><span id="capacity"></span><span id="CAPACITY"></span> 容量

スキーマのパス:\\Printer.Finishing.OutputBins\[ 。TrayName\]: 容量

ノード型: 値

データ型: BIDI\_INT

説明: 現在参照されている出力トレイのシートで、容量。

### <a name="span-idlevelspanspan-idlevelspan-level"></a><span id="level"></span><span id="LEVEL"></span> レベル

スキーマのパス:\\Printer.Finishing.OutputBins\[ 。TrayName\]: レベル

ノード型: 値

データ型: BIDI\_INT

説明: に対する割合で表した、現在参照されている出力トレイに残っている容量です。 空のトレイが 0 の値を持つ完全なトレイの 100 の値です。 レベルが測定可能でない場合は-1 (不明なレベルを示す) の値が返されます。

 

 




