---
title: 赤外線ポートに接続されているプリンター
description: 赤外線ポートに接続されているプリンター
ms.assetid: 8545cf66-9b5c-41e8-82e0-e0edd75ad41b
keywords:
- 赤外線ポート WDK プリンター
- 赤外線ポート WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14311a13add007c681bbf34f69c934f4162755a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354828"
---
# <a name="printer-connected-to-an-infrared-port"></a>赤外線ポートに接続されているプリンター





赤外線 (IR) ポート経由で接続されているプリンターでは、1284 デバイスの文字列を使用して、プラグ アンド プレイをサポートしていません。 赤外線ポートを使用しているコンピューターでのサービスは、常にデバイスをポーリングします。 列挙型では、PDO は作成、IR のプラグ アンド プレイ プリンターが範囲内になる\\ルート\\で、*デバイス ID*フォーム HWP の*nnnn*します。 *ハードウェア ID*の*devnode* HWP フォームの 1 つのエントリが*nnnn*します。

[ **INF 製造元セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547454) lpt ポートと赤外線ポート経由でプラグ アンド プレイをサポートしているプリンターのエントリは、次のような表示する必要があります。

```cpp
 
"Model Name XYZ" = Install_Section_XYZ, LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234, Model_Name_XYZ
"Model Name XYZ" = Install_Section_XYZ, HWP9876, Model_Name_XYZ
```

 

 




