---
title: 一時的なマルチ モニター マネージャーのサポート
description: 一時的なマルチ モニター マネージャーのサポート
ms.assetid: 5091fe00-76d9-4585-9ef0-4b5b7ab8bc06
keywords:
- 一時的なマルチモニターマネージャーの WDK ディスプレイ
- TMM WDK ディスプレイ
- 複製ビュー WDK 表示
- モバイルデバイス WDK、TMM のサポート
- 監視構成 WDK ディスプレイ、TMM サポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6d2f0f92b0b6481c66c717d8e4da6956e91dbcc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825579"
---
# <a name="supporting-transient-multi-monitor-manager"></a>一時的なマルチ モニター マネージャーのサポート


一時的なマルチモニターマネージャーは、モバイルコンピューターでの表示構成のセットアップを簡略化する Windows Vista の機能です。 TMM は、新しいモニターが検出されたときに、モバイルコンピューターの表示 (ラップトップコンピューターの表示など) を複製ビューに配置できます。 デスクトップコンピューターでは、TMM は無効になっています。 Windows Vista では、アプリケーションが複製ビューを開始するために呼び出すことができる GDI 関数はありません。 ハードウェアベンダーは、引き続き独自の独自の方法を使用して、デスクトップコンピューターに複製ビューを入力する必要があります。 ただし、ハードウェアベンダーは、 [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) COM インターフェイスオブジェクトを実装して提供する必要があります。これにより、tmm はモバイルコンピューターで複製ビューモードを設定できます。

このセクションの内容:

[TMM の用語](tmm-terminology.md)

[IViewHelper の複製ビュー COM オブジェクトの要件](requirements-of-an-iviewhelper-clone-view-com-object.md)

[IViewHelper の複製ビュー COM オブジェクトの使用](using-an-iviewhelper-clone-view-com-object.md)

[モニターの構成の処理](handling-monitor-configurations.md)

[プラットフォームがモバイルとデスクトップのどちらであるかを判断する](determining-whether-a-platform-is-mobile-or-desktop.md)

 

 





