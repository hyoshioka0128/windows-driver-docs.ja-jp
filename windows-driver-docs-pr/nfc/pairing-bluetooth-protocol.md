---
title: Bluetooth プロトコルのペアリング
description: Bluetooth プロトコルのペアリング
ms.assetid: 6C95CA57-A226-4252-91E2-FAD8F1A0432B
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf19644005a2699408397661795cfe86debca3a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831551"
---
# <a name="pairingbluetooth-protocol"></a>Pairing:Bluetooth プロトコル


"ペアリング: Bluetooth" プロトコルは、Bluetooth OOB ペアリング構造のサブスクリプションを抽象化する手段です。 Windows は、近接してトリガーされた Bluetooth simple OOB ペアリングを完了するために、Windows が Bluetooth OOB ペアリング構造を受け取ることに関心があるプロバイダーに登録するために、この型をサブスクライブします。

ペアリングのパブリケーションの動作  Bluetooth が定義されていない**ことに注意**してください。

 

**  NFC**対応の NFP プロバイダーの場合、定義された両方の形式 (静的な接続での単一の Bluetooth 通信事業者と簡略化されたタグ形式) がサポートされている必要があります。 ネゴシエートされた接続の引き渡しはサポートされていません。

 

### <a name="required-actions"></a>必要なアクション

-   近接通信テクノロジが NFC として提供されている場合、ドライバーは "ペアリング: Bluetooth" プロトコルのサブスクリプションと、TNF field 値が0x02 で、TYPE フィールドが "application/NDEF" であることを照合する必要があります。

    ドライバーは、NDEF レコードのペイロードのみをこの型のサブスクライバーに返す必要があります。

-   近接通信テクノロジが NFC として提供されている場合、ドライバーは "ペアリング: Bluetooth" プロトコルのサブスクリプションと NDEF メッセージを照合する必要があります。この場合、最初のレコードの TNF フィールドの値が0x01、"Hs" に等しい型フィールド、および単一の代替となります。Bluetooth 通信事業者の構成レコード (mime の種類 "application/vnd") を指す通信会社のレコード。
    -   ドライバーは、この種類のサブスクライバーに "application/vnd. NDEF" レコードのペイロードのみを返す必要があります。
    -   ドライバーは、静的な接続の引き渡しだけをサポートする必要があります。 このドライバーは、ネゴシエートされた接続の引き渡しなど、接続の引き渡し内の他のメカニズムをサポートしていない必要があります。
    -   詳細については、「\[NFC BTSSP\]」を参照してください。
-   ドライバーは、"ペアリング: Bluetooth" の種類の公開をサポートしている場合があります。 このパブリケーション形式は、NFC では定義されていません。
-   ドライバーは、他の互換性のあるスキームもサポートしている可能性があります。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

