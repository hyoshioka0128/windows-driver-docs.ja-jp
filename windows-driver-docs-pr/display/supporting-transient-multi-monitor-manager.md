---
title: 一時的なマルチ モニター マネージャーのサポート
description: 一時的なマルチ モニター マネージャーのサポート
ms.assetid: 5091fe00-76d9-4585-9ef0-4b5b7ab8bc06
keywords:
- 一時的なマネージャー WDK のマルチ モニターの表示
- TMM WDK の表示
- WDK を表示するビューを複製します。
- WDK のモバイル デバイス、TMM サポート
- モニターの構成の WDK 表示、TMM サポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35d3ce0e1463f832fa04b3a5dbd9d24d83d69202
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361215"
---
# <a name="supporting-transient-multi-monitor-manager"></a>一時的なマルチ モニター マネージャーのサポート


マルチ モニターの一時的なマネージャーは、モバイル コンピューターでの表示構成のセットアップを簡素化する Windows Vista の機能です。 新しいモニターが検出されたときに、TMM は複製ビューにモバイル コンピューターのディスプレイを (たとえば、ラップトップ コンピューター ディスプレイ) に配置できます。 TMM はデスクトップ コンピューター上で無効になります。 Windows vista の場合は、複製のビューを入力するアプリケーションを呼び出すことができる GDI 関数はありません。 ハードウェア ベンダーは、自分独自の方法を使用して、デスクトップ コンピューターに複製ビューの入力を続ける必要があります。 ただし、ハードウェア ベンダーが実装する必要があります、提供、 [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) TMM モバイル コンピューターに複製表示モードを設定すると、COM インターフェイスのオブジェクト。

このセクションの内容:

[TMM 用語集](tmm-terminology.md)

[IViewHelper 複製ビュー COM オブジェクトの要件](requirements-of-an-iviewhelper-clone-view-com-object.md)

[IViewHelper 複製-ビューの COM オブジェクトを使用します。](using-an-iviewhelper-clone-view-com-object.md)

[処理モニターの構成](handling-monitor-configurations.md)

[確認するかどうか、プラットフォーム、モバイルまたはデスクトップ](determining-whether-a-platform-is-mobile-or-desktop.md)

 

 





