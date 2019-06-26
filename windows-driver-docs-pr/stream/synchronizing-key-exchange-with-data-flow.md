---
title: キー交換とデータ フローの同期
description: キー交換とデータ フローの同期
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
ms.openlocfilehash: 4964b70bb285950e0dff19fdba6f6825d0d6ffda
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377748"
---
# <a name="synchronizing-key-exchange-with-data-flow"></a>キー交換とデータ フローの同期





前のキーからすべてのデータが処理される前に、キーの交換プロセスを開始可能性があります。 この例は、セットでいくつかのムービー設定メイン プログラムのタイトルにトレーラー タイトルからの移行になります。 フラグがある、 **TypeSpecificFlags**のメンバー、 [ **KSSTREAM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)各データ パケットの構造体。 このフラグは**KS\_AM\_UseNewCSSKey**、定義されている*ksmedia.h*します。 ヘッダーの直後に続くデータ サンプルが新しいタイトル キーを適用する最初のデータ サンプルであることを示します。

復号化には、古いキーを使用中に新しいキーの交換を処理できますが、プロパティを受信すると、DVD デコーダーのミニドライバーは、キーの交換を処理する必要があります。 すべてのムービー データまで、前のキーを必要とする処理が完了し、復号化の SRB を保持する場合は、復号化を待機する必要があります、**設定**プロパティ。 復号化を使用して、 [ **KS\_DVDCOPY\_設定\_コピー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)パラメーターを使用した構造**KS\_DVDCOPYSTATE\_初期化**または**KS\_DVDCOPYSTATE\_初期化\_タイトル**が受信されるまで、 **KS\_AM\_UseNewCSSKey**フラグをそれに接続されているすべてのストリーム。 その後は、DVD デコーダーのミニドライバーは、その時点までに受信したすべてのパケットを処理します。 これにより、不正なキーを使用してデータになります。

 

 




