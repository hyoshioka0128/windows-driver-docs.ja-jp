---
title: データ フローとキー交換の同期
description: データ フローとキー交換の同期
ms.assetid: 54abc258-d26a-4d42-a5aa-712cdae76b6d
keywords:
- DVD デコーダー ミニドライバー WDK、著作権保護
- デコーダー ミニドライバー WDK DVD、著作権保護
- 著作権保護 WDK DVD デコーダー
- キー交換 WDK DVD デコーダー
- WDK DVD デコーダーの復号化
- 暗号化の WDK DVD デコーダー
- 暗号化の WDK DVD デコーダー
- DVD decrypters WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a46dd2a8bacef749819c0878a2a5fc780e1d0a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531987"
---
# <a name="synchronizing-key-exchange-with-data-flow"></a>データ フローとキー交換の同期





前のキーからすべてのデータが処理される前に、キーの交換プロセスを開始可能性があります。 この例は、セットでいくつかのムービー設定メイン プログラムのタイトルにトレーラー タイトルからの移行になります。 フラグがある、 **TypeSpecificFlags**のメンバー、 [ **KSSTREAM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567138)各データ パケットの構造体。 このフラグは**KS\_AM\_UseNewCSSKey**、定義されている*ksmedia.h*します。 ヘッダーの直後に続くデータ サンプルが新しいタイトル キーを適用する最初のデータ サンプルであることを示します。

復号化には、古いキーを使用中に新しいキーの交換を処理できますが、プロパティを受信すると、DVD デコーダーのミニドライバーは、キーの交換を処理する必要があります。 すべてのムービー データまで、前のキーを必要とする処理が完了し、復号化の SRB を保持する場合は、復号化を待機する必要があります、**設定**プロパティ。 復号化を使用して、 [ **KS\_DVDCOPY\_設定\_コピー\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567639)パラメーターを使用した構造**KS\_DVDCOPYSTATE\_初期化**または**KS\_DVDCOPYSTATE\_初期化\_タイトル**が受信されるまで、 **KS\_AM\_UseNewCSSKey**フラグをそれに接続されているすべてのストリーム。 その後は、DVD デコーダーのミニドライバーは、その時点までに受信したすべてのパケットを処理します。 これにより、不正なキーを使用してデータになります。

 

 




