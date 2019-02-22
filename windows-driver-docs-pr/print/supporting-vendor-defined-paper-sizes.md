---
title: ベンダー定義用紙サイズのサポート
description: ベンダー定義用紙サイズのサポート
ms.assetid: 5c356857-ef43-41e4-a4ed-fae6655bd9ce
keywords:
- WDK Unidrv のベンダーから提供された用紙サイズします。
- WDK Unidrv の非標準の用紙サイズします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3962d8c19760145cceb7d4e818d8d2cea6213d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550192"
---
# <a name="supporting-vendor-defined-paper-sizes"></a>ベンダー定義用紙サイズのサポート





ベンダー定義用紙サイズはベンダー固有であり、各プリンターの GPD ファイルで完全に記述する必要があります。 これらのサイズとも呼ばれます、非標準の用紙サイズに含まれないため、[標準オプション](standard-options.md)PaperSize 機能。

プリンターがサポートする各ベンダー定義用紙サイズの用紙サイズ、GPD ファイルの機能を含める必要があります、\*エントリの引数がない、標準的なオプション名のいずれかのオプションします。 このエントリで、次のオプション属性が必要です。

\*PageDimensions \*PrintableArea \*PrintableOrigin \*rcNameID または\*名前\*コマンドを次のオプション属性が、使用できますが、必須ではありません。

\*CursorOrigin \*RotateSize でしょうか。
\*PageProtectMem
 

 




