---
title: ハード ディスク
description: ハード ディスク
ms.assetid: 88eadea0-54cb-4c19-90d2-9941b13b9303
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aff1b423946c6011954835c32aa4e1f8e83f56e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360534"
---
# <a name="harddisk"></a>ハード ディスク


スキーマのパス:\\Printer.Configuration.HardDisk

ノード型: プロパティ

説明: デバイスにインストールされているハード_ディスクの値のエントリ。

ハード ディスク プロパティには、次の 3 つの子の値が含まれています。容量と空き容量は、インストールされます。

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> インストールされています。

スキーマのパス:\\Printer.Configuration.HardDisk:Installed

ノード型: 値

データ型: BIDI\_BOOL

説明: デバイスのハード_ディスクがインストールされているかどうかを示します。 場合**TRUE**、ハード ディスクがインストールされている場合は**FALSE**、ハード ディスクがインストールされていません。

### <a name="span-idcapacityspanspan-idcapacityspan-capacity"></a><span id="capacity"></span><span id="CAPACITY"></span> 容量

スキーマのパス:\\Printer.Configuration.HardDisk:Capacity

ノード型: 値

データ型: BIDI\_INT

説明: メガバイト (MB)、インストールされているハード_ディスクの容量。

### <a name="span-idfreespacespanspan-idfreespacespan-freespace"></a><span id="freespace"></span><span id="FREESPACE"></span> FreeSpace

スキーマのパス:\\Printer.Configuration.HardDisk:FreeSpace

ノード型: 値

データ型: BIDI\_INT

説明: インストールされているハード_ディスクの現在使用可能な空き領域をメガバイト (MB)。

 

 




