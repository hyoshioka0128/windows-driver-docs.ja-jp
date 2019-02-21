---
title: GDI 指定ハーフトーン
description: GDI 指定ハーフトーン
ms.assetid: c7f3d148-4620-4060-bbf8-253e9e35c397
keywords:
- GDI 指定ハーフトーン WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c0c9abbdf8db43f14fbd86a9bda5e29ca72bca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536597"
---
# <a name="gdi-supplied-halftoning"></a>GDI 指定ハーフトーン





かどうか、指定した色形式は 1 ピクセルあたりのビット数が、イメージの描画に使用されているいずれか (\*DrvBPP) プリンターでサポートが 1 ピクセルあたりのビットの場合と同じ (\*DevBPP を乗算して\*DevNumOfPlanes)、し、ハーフトーン操作は、GDI によって処理されます。 例としてを\*、4 つの値を DrvBPP で\*DevBPP 1 に等しいと\*DevNumOfPlanes が 4 に等しい。

このような状況では、ハーフトーン メソッドのみが許可される GDI を提供します。 これらのハーフトーン メソッドが下に示されている標準的なハーフトーン オプション名を使用して GPD ファイルで表される[標準オプション](standard-options.md)します。 Unidrv、プリンターのために使用する GDI でサポートされているハーフトーン メソッドを指定するには、その名前を指定\*ハーフトーン機能のエントリのオプションします。 (ハーフトーン機能は、標準の 1 つ[プリンターの機能](printer-features.md))。

ハーフトーン メソッドはどの色のモードの使用を選択できるを制限する場合、GPD ファイルで複数のハーフトーン メソッドとカラー モードを指定する場合と[制約オプション](option-constraints.md)します。

Unidrv は標準の HT\_PATSIZE\_GPD ファイル ハーフトーン オプションが指定されていない場合、AUTO オプション。 HT\_PATSIZE\_自動オプションを選択した解像度と色のモードについて最適である標準のハーフトーン メソッドを使用して Unidrv 指定とします。 これにより、ユーザーが任意の特定の組み合わせの最適なハーフトーン オプションを理解する必要はありません、解像度と色のモードのさまざまな組み合わせの間での切り替えができます。

ハーフトーンの GDI が指定した機能を使用するには、する場合は、指定[ハーフトーンのミニドライバーが指定したパターン](minidriver-supplied-halftone-patterns.md)します。

色の形式の詳細については、次を参照してください。[色形式の処理](handling-color-formats.md)します。

 

 




