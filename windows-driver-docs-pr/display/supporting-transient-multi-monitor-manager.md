---
title: マルチ モニターの一時的なマネージャーのサポート
description: マルチ モニターの一時的なマネージャーのサポート
ms.assetid: 5091fe00-76d9-4585-9ef0-4b5b7ab8bc06
keywords:
- 一時的なマネージャー WDK のマルチ モニターの表示
- TMM WDK の表示
- WDK を表示するビューを複製します。
- WDK のモバイル デバイス、TMM サポート
- モニターの構成の WDK 表示、TMM サポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c0c9e6a3c68c6c9ec944c25e8976c5fd98b9fda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532685"
---
# <a name="supporting-transient-multi-monitor-manager"></a>マルチ モニターの一時的なマネージャーのサポート


マルチ モニターの一時的なマネージャーは、モバイル コンピューターでの表示構成のセットアップを簡素化する Windows Vista の機能です。 新しいモニターが検出されたときに、TMM は複製ビューにモバイル コンピューターのディスプレイを (たとえば、ラップトップ コンピューター ディスプレイ) に配置できます。 TMM はデスクトップ コンピューター上で無効になります。 Windows vista の場合は、複製のビューを入力するアプリケーションを呼び出すことができる GDI 関数はありません。 ハードウェア ベンダーは、自分独自の方法を使用して、デスクトップ コンピューターに複製ビューの入力を続ける必要があります。 ただし、ハードウェア ベンダーが実装する必要があります、提供、 [IViewHelper](https://msdn.microsoft.com/library/windows/hardware/ff568164) TMM モバイル コンピューターに複製表示モードを設定すると、COM インターフェイスのオブジェクト。

このセクションの内容:

[TMM 用語集](tmm-terminology.md)

[IViewHelper 複製ビュー COM オブジェクトの要件](requirements-of-an-iviewhelper-clone-view-com-object.md)

[IViewHelper 複製-ビューの COM オブジェクトを使用します。](using-an-iviewhelper-clone-view-com-object.md)

[処理モニターの構成](handling-monitor-configurations.md)

[確認するかどうか、プラットフォーム、モバイルまたはデスクトップ](determining-whether-a-platform-is-mobile-or-desktop.md)

 

 





