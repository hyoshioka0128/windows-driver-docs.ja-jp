---
title: Windows メモリ領域の概要
description: Windows メモリ領域の概要
ms.assetid: b49a35c2-6da6-4239-a67b-542d42a5c9e4
keywords:
- メモリの領域について、メモリ管理の WDK カーネル
- メモリ領域の WDK カーネル
- 物理メモリの WDK カーネル
- 仮想メモリの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5773a3afab3cbd857cf86b25085b36de86b9f6f3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377930"
---
# <a name="overview-of-windows-memory-space"></a>Windows メモリ領域の概要





次の図は、NT ベースのオペレーティング システムの仮想メモリ スペースとシステムの物理メモリを関係を示しています。

![図に示す仮想メモリ空間と物理メモリ](images/16vrtmem.gif)

この図に示すようには、仮想メモリはページの物理メモリによってバックアップされ、仮想アドレスの範囲は連続していない物理メモリのページでバックアップできます。 ユーザー スペースの仮想メモリとページ プールから割り当てられたメモリをシステム領域は、常に*ページング可能な*します。 任意のユーザー領域のコードまたはデータ ページ アウトできますセカンダリ ストレージにいつでも、プロセスが実行中であってもします。

そのメモリ領域にアクセスできないため、固定のプロセス仮想アドレスは表示されずに注意してください。

メモリ管理の広範なについては、次を参照してください。、*内では、Microsoft Windows Internals*マイクロソフト プレスの書籍。

 

 




