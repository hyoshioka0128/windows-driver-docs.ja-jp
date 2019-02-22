---
title: デュアル (Windows 2000 モデル) をサポートしています。
description: デュアル (Windows 2000 モデル) をサポートしています。
ms.assetid: 08da97c9-1d31-40f5-99df-5f16eaa47c79
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、デュアル ビュー
- デュアル WDK ビデオのミニポート
- 複数のディスプレイ デバイス ビデオのミニポートを同時に WDK
- SingleView WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d90d09e2e0ed83cd554c1c932e21767d4da2c29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557668"
---
# <a name="supporting-dualview-windows-2000-model"></a>デュアル (Windows 2000 モデル) をサポートしています。


多くの最新のディスプレイ アダプターは、2 つ以上の別のディスプレイ デバイスのドライブを同時にできます。 デュアル ビュー、および後で、Microsoft Windows XP の機能は、マルチ モニターのと同様の機能をシステム レベルのサポートを提供しますが、1 つのディスプレイ アダプターのみが必要です。 グラフィックス デバイス インターフェイス (GDIs) とエンドユーザーのエクスペリエンスは、同じデュアル ビューとマルチ モニターの両方です。

SingleView モード

SingleView モードでは、ディスプレイ アダプターは、モニターの数に関係なく、1 つのディスプレイ デバイスをドライブします。 これは、Windows 2000 およびそれ以降のオペレーティング システム バージョンがサポートされているディスプレイ アダプターのほとんどの通常モードです。

デュアル モード

デュアル モードのコンピューターでは、各ディスプレイ デバイスがデスクトップの別の部分ビューの一種で別のモニターで複数のイメージをドライブ (複数のビデオ ポート) を持つ 1 つのディスプレイ アダプターを使用できます。 プライマリ画像が表示されます、*プライマリ ビュー*; その他のイメージを表示*セカンダリ ビュー*します。

次のサブセクションでは、デュアル ビューの詳細についてを説明します。

[デュアル ビューを有効にします。](enabling-dualview.md)

[実装の詳細を高度なデュアル ビュー](dualview-advanced-implementation-details.md)

 

 





