---
title: ミニポート ドライバー ハードウェア リセット
description: ミニポート ドライバー ハードウェア リセット
ms.assetid: d5209809-039c-4ac2-afdf-1f5144307850
keywords:
- ネットワークインターフェイスカード WDK ネットワーク、リセット
- Nic WDK ネットワーク、リセット
- NIC のリセット
- MiniportResetEx
- ハードウェアのリセット WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a838a33bcd8c338541b90db37d1ff713cb4caa6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842548"
---
# <a name="miniport-driver-hardware-reset"></a>ミニポート ドライバー ハードウェア リセット





ミニポートドライバーは、 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)を使用して[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数を登録する必要があります。

*Miniportresetex*は、 [**NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)の呼び出しを使用して同期的または非同期的に完了できます (次の図を参照)。

![ネットワークインターフェイスカードのリセットを示す図](images/207-09.png)

*Miniportresetex*が必要:

-   さらに割り込みを無効にします。

-   進行中の送信に関連付けられているデータをクリアします。 たとえば、バスマスタダイレクトメモリアクセス (DMA) デバイスのリングバッファーでは、送信バッファーへのポインターをクリアする必要があります。 逆シリアル化された接続指向ミニポートドライバーは、キューに置かれた送信要求に対して要求\_中止さ\_、NDIS\_ステータスを返す必要があります。

-   ハードウェアの状態とミニポートドライバーの内部状態を、リセット操作前の状態に復元します。

ミニポートドライバーは、マルチキャストアドレス、パケットフィルター、タスクオフロード設定、およびウェイクアップパターンを除き、デバイスのハードウェア状態を復元する役割を担います。 これらの設定は、ミニポートドライバーまたは NDIS によって復元されます。 このミニポートドライバーは、 *Addressingreset*パラメーターでブール値を返すことによって、これらの設定を復元する担当者を決定します。

アドレスポートドライバーが*Addressingreset*パラメーターで**FALSE**を返す場合、ミニポートドライバーは、マルチキャストアドレス、パケットフィルター、タスクオフロード設定、およびウェイクアップパターンを初期状態に復元します。 このミニポートドライバーが*Addressingreset*で**TRUE**を返した場合、NDIS は、コネクションレスのミニポートドライバーの[*miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数または接続指向ミニポートドライバーの[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数を呼び出して、次の構成設定:

-   OID\_GEN の set 要求を使用したネットワークパケットフィルターは、[現在の\_パケット\_フィルター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)ます。

-   OID の set 要求を使用したマルチキャストアドレスリスト[\_802\_3\_マルチキャスト\_リスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-multicast-list)。

-   [OID\_オフロード\_カプセル](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)化の設定要求によって、タスクのカプセル化をオフロードします。

-   \_PNP の set 要求を使用した電源管理のウェイクアップパターン[\_\_ウェイクアップ\_up\_パターンを追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)します。
    **注**  NDIS 6.20 以降では、OID\_PM を使用して設定されたウェイクアップパターン[\_\_WOL\_パターンを追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)して、ミニポートドライバーで復元する必要があります。

     

## <a name="related-topics"></a>関連トピック


[ミニポートドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)

[ミニポートアダプターの状態と操作](miniport-adapter-states-and-operations.md)

[ミニポートドライバーのリセットと停止の機能](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564064(v=vs.85))

 

 






