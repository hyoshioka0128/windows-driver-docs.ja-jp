---
title: セクション オブジェクトとビュー
description: セクション オブジェクトとビュー
ms.assetid: 9c60b761-6326-4d1a-b884-cc2acee4bedd
keywords:
- メモリ管理の WDK カーネル、セクション オブジェクト
- メモリ管理の WDK カーネル、共有メモリ
- WDK のカーネルを共有メモリ
- セクション オブジェクト WDK カーネル
- メモリのセクションでは WDK カーネル
- メモリ アドレス空間の共有
- ビューの WDK メモリ セクション
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 215aa48e7af3a94377b7e775da1e21ba47bd61f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377297"
---
# <a name="section-objects-and-views"></a>セクション オブジェクトとビュー





A*セクション オブジェクト*共有可能なメモリのセクションを表します。 プロセスでは、セクション オブジェクトを使用して、その他のプロセスのメモリ アドレス空間 (メモリのセクション) の一部を共有します。 セクション オブジェクトでは、使用されるプロセスは、そのメモリ アドレス空間にファイルをマップできますメカニズムも提供します。

各メモリ セクションには対応する 1 つまたは複数*ビュー*します。 セクションのビューは、プロセスに実際に表示されているセクションの一部です。 セクションと呼ばれるは、ビューを作成するの act*マッピング*セクションのビュー。 各セクションの内容を操作するプロセスが独自のビュープロセスは複数のビューを (同じまたは別のセクションで) することもできます。

このセクションでは、次のトピックについて説明します。

[ファイル バックアップし、ファイルに格納されたページのセクション](file-backed-and-page-file-backed-sections.md)

[メモリのセクションを管理します。](managing-memory-sections.md)

[セクション オブジェクトとビューに関するセキュリティの問題](security-issues-for-section-objects-and-views.md)

 

 




