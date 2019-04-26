---
title: Bluetooth のプロトコルのペアリング
description: Bluetooth のプロトコルのペアリング
ms.assetid: 6C95CA57-A226-4252-91E2-FAD8F1A0432B
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f185a04d31ab54d2931a97a774e23c41643b0852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348565"
---
# <a name="pairingbluetooth-protocol"></a>Pairing:Bluetooth プロトコル


ペアリング: Bluetooth"プロトコルは、Bluetooth OOB ペアリング構造体のサブスクリプションを抽象化の手段です。 Windows は、Windows が近接によってトリガーされる Bluetooth 単純な OOB のペアリングが完了するには構造体をペアリング Bluetooth OOB を受信することに興味を示しているプロバイダーに登録するには、この型にサブスクライブします。

**注**  ペアリング: Bluetooth のパブリケーションの動作は未定義

 

**注**  の NFC 対応 NFP プロバイダーでは、両方の定義の形式 (静的接続引き渡し単一 Bluetooth キャリアとタグの形式の簡略化) をサポートする必要があります。 ネゴシエートされた接続の引き渡しはサポートされていない必要があります。

 

### <a name="required-actions"></a>必要な操作

-   近接テクノロジが NFC としてアドバタイズされる場合、ドライバーは 0x02 TNF フィールド値を持つ NDEF メッセージと"application/vnd.bluetooth.ep.oob"に相当する型のフィールドが"ペアリング: Bluetooth"プロトコルのサブスクリプションと一致する必要があります。

    ドライバーは、この種類のサブスクライバーに NDEF レコードのペイロードのみを返す必要があります。

-   NFC、し、ドライバーする必要があります"ペアリング: Bluetooth"プロトコルの最初のレコードが 0x01 の TNF フィールドの値を持つ NDEF メッセージのサブスクリプションと一致も近接テクノロジが提供されると場合、型フィールドと等しい"h"、および 1 つの代替手段Bluetooth 通信事業者の構成レコード (mime タイプ"application/vnd.bluetooth.ep.oob") を参照する運送業者のレコードです。
    -   ドライバーは、この種類のサブスクライバーに"application/vnd.bluetooth.ep.oob"NDEF レコードのペイロードのみを返す必要があります。
    -   ドライバーは、静的な接続の引き渡しのみをサポートする必要があります。 MUST NOT ドライバーでは、接続のネゴシエート引き渡しなどの接続の引き渡し内の他のメカニズムをサポートします。
    -   参照してください\[NFC BTSSP\]詳細についてはします。
-   ドライバーは、"ペアリング: Bluetooth"の種類のパブリケーションをサポート可能性があります。 このパブリケーションの形式は、NFC の定義されていません。
-   ドライバーは、その他の互換性のあるスキームもをサポート可能性があります。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

