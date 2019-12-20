---
title: UMDF ドライバーでの割り込みの処理
description: 割り込みの処理
ms.assetid: 5C8CB68A-EAE6-4AF9-8B10-F8B73B50DEB2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50ceb50c4efb3d224a49c6aeebc498d0c7f08da
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209928"
---
# <a name="handling-interrupts-in-umdf-drivers"></a>UMDF ドライバーでの割り込みの処理


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

UMDF バージョン1.11 以降では、UMDF ドライバーはハードウェア割り込みを処理できます。 UMDF では、行ベース (レベルトリガとエッジトリガの両方) とメッセージシグナル (MSI) 割り込みの両方がサポートされています。

レベルでトリガーされる行ベースの割り込みは、Windows 8 以降で使用できます。 MSI とラインベースのエッジによってトリガーされる割り込みは、UMDF 1.11 がサポートするすべてのオペレーティングシステムで使用できます。

フレームワークベースのドライバーは、フレームワークの割り込みオブジェクトを使用して、ハードウェアの割り込みを管理します。

## <a name="in-this-section"></a>このセクションの内容


-   [Interrupt オブジェクトの作成](creating-an-interrupt-object-umdf.md)
-   [割り込みの有効化と無効化](enabling-and-disabling-interrupts-umdf.md)
-   [割り込みの処理](servicing-an-interrupt-umdf.md)
-   [作業項目の使用](using-workitems.md)
-   [同期 (割り込みコードを)](synchronizing-interrupt-code-umdf.md)
-   [Interrupt オブジェクトの削除](deleting-an-interrupt-object.md)

 

 





