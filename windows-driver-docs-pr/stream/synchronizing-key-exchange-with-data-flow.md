---
title: キー交換とデータ フローの同期
description: キー交換とデータ フローの同期
ms.assetid: 54abc258-d26a-4d42-a5aa-712cdae76b6d
keywords:
- DVD デコーダーミニドライバー WDK、著作権保護
- デコーダーミニドライバー WDK DVD、著作権保護
- 著作権保護 WDK DVD デコーダー
- キー交換 WDK DVD デコーダー
- 暗号化解除 WDK DVD デコーダー
- 暗号化 WDK DVD デコーダー
- 暗号化 WDK DVD デコーダー
- DVD decrypters WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4ff0c369f0512976a4c980fe29977a0676b17c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843589"
---
# <a name="synchronizing-key-exchange-with-data-flow"></a>キー交換とデータ フローの同期





キー交換プロセスは、前のキーからのすべてのデータが処理される前に開始される場合があります。 この例として、トレーラーのタイトルセットから、いくつかのムービーで設定されているメインプログラムタイトルに移行することが挙げられます。 各データパケットの**TypeSpecificFlags**メンバーには、 [**KSK ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造体のフラグがあります。 このフラグは、UseNewCSSKey で定義されている**KS\_AM\_** *です。* これは、そのヘッダーの直後にあるデータサンプルが、新しいタイトルキーが適用される最初のデータサンプルであることを示しています。

古いキーを使用しているときに decrypter が新しいキー交換を処理できる場合、DVD デコーダーミニドライバーは、プロパティを受信するときにキー交換を処理する必要があります。 前のキーを必要とするすべてのムービーデータが処理されるまで decrypter が待機する必要がある場合、decrypter は**Set**プロパティの SRB を保持します。 Decrypter は、 [**ks\_\_DVDCOPY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)を使用して\_状態構造\_コピーします。パラメーターには、 **DVDCOPYSTATE\_Initialize**または**ks\_DVDCOPYSTATE\_initialize を使用します。** 接続されているすべてのストリームで**KS\_AM\_UseNewCSSKey**フラグを受信するまでのタイトル。 その後、DVD デコーダーミニドライバーは、その時点までに受信したすべてのパケットを処理します。 これにより、データに正しくないキーを使用できなくなります。

 

 




