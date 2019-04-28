---
title: 1394 構成 ROM の修正
description: 1394 構成 ROM の修正
ms.assetid: 3dc4fe53-a26b-44c7-96ef-e7bb6181c958
keywords:
- IEEE 1394 WDK バス、Rom の構成を変更します。
- 1394 WDK バス、Rom の構成を変更します。
- Rom WDK の IEEE 1394 バスの構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5715354142e237460d5959926ae813a2f5c0b60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370986"
---
# <a name="modifying-the-1394-configuration-rom"></a>1394 構成 ROM の修正





1394 バスに接続されている Microsoft Windows システムでは、ノードでサポートされている機能のユニットを説明する構成 ROM を公開します。 1394 構成 Rom の詳細については、IEEE 1394 1995 と IEEE-1212 2000 仕様を参照してください。 Windows XP およびそれ以降のオペレーティング システムでは、2 つの方法で構成 ROM の内容が動的に定義することができます。

1.  ドライバーでは、1394 バス上の非 1394 バス用に設計されたハードウェアを公開する構成 ROM を動的に変更できます。

    たとえば、汎用システム、システムの IDE バスに接続されている内部の DVD ドライブを検討してください。 DVD ドライブで使用されるプロトコルに 1394 要求をマップするドライバーは、1394 の他のノードに 1394 バス上の DVD ドライブにさらされる可能性が。 これを行うことには、システムの 1394 構成 ROM に単位の新しいディレクトリを追加する必要があります。 1394 バスに接続されているその他のシステムは、1394 DVD デバイスの場合と同様に、汎用システムを列挙することになります。

2.  ドライバーは、仮想の物理デバイス オブジェクト (Pdo) を使用して、デバイス ドライバーのテストを容易にするための方法でハードウェアをエミュレートします。

    デバイスのエミュレーションでは、まだ受信がいないデバイスのドライバーをテストできます。 ハードウェア エミュレーション ドライバーは、1394 バス上の仮想 1394 デバイスに公開できます。 開発者は、別のシステムで新しいハードウェアのドライバーをデバッグできます。 詳細については、デバイスのエミュレーションは、次を参照してください。[ハードウェア エミュレーション ドライバーの IEEE 1394](https://msdn.microsoft.com/library/windows/hardware/ff537214)します。

## <a name="related-topics"></a>関連トピック
[IEEE 1394 ノードの構成 ROM の内容を取得します。](https://msdn.microsoft.com/library/windows/hardware/gg266408)  



