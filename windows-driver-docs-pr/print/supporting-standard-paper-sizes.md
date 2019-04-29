---
title: 標準の用紙サイズをサポートする
description: 標準の用紙サイズをサポートする
ms.assetid: 04f8fbdb-88f8-4595-b5d2-74315c02bb41
keywords:
- WDK Unidrv の標準の用紙サイズします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ee3143567a530f06e80f3613a1cf04e57401bd4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331750"
---
# <a name="supporting-standard-paper-sizes"></a>標準の用紙サイズをサポートする





標準の用紙サイズがによって表される、[標準オプション](standard-options.md)PaperSize 機能。

プリンターでサポートされる標準の用紙サイズごとに、GPD ファイルの用紙サイズの機能を含める必要があります、\*エントリ偏角 (CUSTOMSIZE) を除く標準のオプション名のいずれかのオプションします。 このエントリで、次のオプション属性が必要です。

\*PrintableArea \*PrintableOrigin \*rcNameID\*コマンドを次のオプション属性が、使用できますが、必須ではありません。

\*CursorOrigin \*RotateSize でしょうか。
\*すべての標準の用紙サイズを RCID PageProtectMem\_DMPAPER\_システム\_名前のリソース識別子 (stdnames.gpd で定義されている) は、引数として使用する必要があります\* **rcNameID**.

 

 




