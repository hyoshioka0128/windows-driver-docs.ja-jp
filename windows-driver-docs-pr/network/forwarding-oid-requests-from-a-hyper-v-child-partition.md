---
title: Hyper-V 子パーティションからの OID 要求の転送
description: Hyper-V 子パーティションからの OID 要求の転送
ms.assetid: 35EA9964-4CD0-4636-9573-65F37393B7E2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e093a82a2e661526b204bcb55d2866a2bcd59f4c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841750"
---
# <a name="forwarding-oid-requests-from-a-hyper-v-child-partition"></a>Hyper-V 子パーティションからの OID 要求の転送


Oid\_802\_3 を含むマルチキャストオブジェクト識別子 (OID) 要求[\_\_マルチキャスト\_アドレス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-add-multicast-address)および[OID\_802\_3\_削除\_マルチキャスト\_アドレス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-delete-multicast-address)は、次のように実行されるプロトコルとフィルタードライバーによって発行されます。

-   Hyper-v の親パーティションで実行されている管理オペレーティングシステム。

-   Hyper-v 子パーティションで Windows Vista 以降のバージョンの Windows オペレーティングシステムを実行しているゲストオペレーティングシステム。

拡張可能スイッチインターフェイスは、これらの OID 要求を拡張可能なスイッチ制御パスに転送します。 これにより、拡張機能がパーティションで使用されているネットワークインターフェイスに関する構成情報を取得できるようになります。

たとえば、拡張スイッチのプロトコルエッジは oid セット要求\_802\_3\_転送し、子パーティションから拡張可能なスイッチコントロールパスの下に[\_マルチキャスト\_アドレスを追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-add-multicast-address)します。 これにより、拡張機能は、そのパーティションのネットワークインターフェイスで使用されるマルチキャストアドレス構成を取得できます。

これらのマルチキャスト OID 要求が拡張可能スイッチインターフェイスに到着すると、拡張可能スイッチのプロトコルエッジは、 [**NDIS\_スイッチ\_NIC\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造内に oid 要求をカプセル化します。 また、プロトコルエッジは、この構造体のメンバーを次のように設定します。

-   **SourcePortId**と**Sourcenicindex**のメンバーは、OID 要求の送信元のパーティションによって使用されるポートおよびネットワークアダプターの対応する値に設定されます。

    **注**  マルチキャスト OID 要求が管理オペレーティングシステムから送信された場合、プロトコルエッジはこれらのメンバーを拡張スイッチ内部ネットワークアダプターの値に設定します。

     

-   **DestinationPortId**メンバーと**DestinationNicIndex**メンバーは0に設定されます。 これは、カプセル化された OID 要求が、コントロールパス内の拡張機能に配信されることを指定します。

-   **OidRequest**メンバーは、カプセル化された oid 要求の[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造のアドレスに設定されます。

次に、プロトコルエッジは[oid\_スイッチ\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)を発行して、カプセル化された oid 要求を拡張可能なスイッチ制御パスに転送します。 基になる転送拡張機能は、カプセル化されたこれらの OID 要求を検査し、指定したマルチキャストアドレス情報を保持できます。 たとえば、拡張可能なスイッチポートに転送するマルチキャストパケットが発生した場合、この情報が必要になることがあります。

拡張可能なスイッチ制御パスの詳細については、「 [Hyper-v 拡張可能スイッチの制御パス](hyper-v-extensible-switch-control-path.md)」を参照してください。

 

 





