---
title: UMDF ドライバーでの割り込みを処理
description: 割り込みの処理
ms.assetid: 5C8CB68A-EAE6-4AF9-8B10-F8B73B50DEB2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0297939bbc09e62fdfb219e3b079fb3548b18c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68229647"
---
# <a name="handling-interrupts-in-umdf-drivers"></a>UMDF ドライバーでの割り込みを処理


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF バージョン 1.11 以降、UMDF ドライバーはハードウェアの割り込みを処理できます。 UMDF は行ベース (両方のレベルによってトリガーされるおよびエッジによってトリガーされる) の両方をサポートし、メッセージ シグナル (MSI) を中断します。

レベルによってトリガーされる、行ベースの割り込みは、以降 Windows 8 で利用可能です。 MSI およびエッジによってトリガーされる、行ベースの割り込み UMDF 1.11 をサポートするすべてのオペレーティング システムで提供されます。

フレームワーク ベースのドライバーでは、ハードウェアの割り込みを管理するためにフレームワーク割り込みオブジェクトを使用します。

## <a name="in-this-section"></a>このセクションの内容


-   [割り込みオブジェクトを作成します。](creating-an-interrupt-object-umdf.md)
-   [有効にして、割り込みを無効化](enabling-and-disabling-interrupts-umdf.md)
-   [割り込みを処理します。](servicing-an-interrupt-umdf.md)
-   [作業項目の使用](using-workitems.md)
-   [割り込みのコードを同期します。](synchronizing-interrupt-code-umdf.md)
-   [割り込みのオブジェクトの削除](deleting-an-interrupt-object.md)

 

 





