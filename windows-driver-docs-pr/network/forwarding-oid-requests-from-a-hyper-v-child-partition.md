---
title: Hyper-V 子パーティションからの OID 要求の転送
description: Hyper-V 子パーティションからの OID 要求の転送
ms.assetid: 35EA9964-4CD0-4636-9573-65F37393B7E2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 044ba4d6dbf61df881eab0d0acf64316d2f9895d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382781"
---
# <a name="forwarding-oid-requests-from-a-hyper-v-child-partition"></a>Hyper-V 子パーティションからの OID 要求の転送


マルチキャストのオブジェクト識別子 (OID) が要求を含む[OID\_802\_3\_追加\_マルチキャスト\_アドレス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-add-multicast-address)と[OID\_802\_3\_削除\_マルチキャスト\_アドレス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-delete-multicast-address)関連プロトコルで発行し、ドライバーが次のように動作するをフィルター処理します。

-   HYPER-V 親パーティションで実行されている管理オペレーティング システム。

-   Windows Vista または Windows オペレーティング システムの以降のバージョンを HYPER-V 子パーティションで実行されているゲスト オペレーティング システム。

拡張可能スイッチのインターフェイスは、拡張可能スイッチ コントロール パスにこれらの OID 要求を転送します。 これにより、パーティションで使用されているネットワーク インターフェイスに関する構成情報を取得する拡張機能です。

拡張可能スイッチのプロトコルのエッジがの OID セット要求を転送するなど、 [OID\_802\_3\_追加\_マルチキャスト\_アドレス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-add-multicast-address)ダウン子パーティションから拡張可能スイッチ コントロールのパス。 これにより、そのパーティション内のネットワーク インターフェイスで使用されるマルチキャスト アドレス構成を取得する拡張機能です。

拡張可能スイッチのプロトコルのエッジが内での OID 要求をカプセル化、拡張可能スイッチのインターフェイスでこれらのマルチキャスト OID 要求が届いたら、 [ **NDIS\_切り替える\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造体。 プロトコルのエッジには、次のようにこの構造体のメンバーも設定します。

-   **SourcePortId**と**SourceNicIndex**メンバーは、OID 要求が発行されたパーティションで使用するポートおよびネットワーク アダプターの対応する値に設定されます。

    **注**  プロトコル エッジが、拡張可能スイッチの内部ネットワーク アダプターの値にこれらのメンバーを設定、マルチキャストの OID 要求は、管理オペレーティング システムから生成されたとき場合、。

     

-   **DestinationPortId**と**DestinationNicIndex**メンバーが 0 に設定します。 これは、カプセル化された OID 要求がコントロール パスの拡張機能に配信されることを指定します。

-   **OidRequest**メンバーのアドレスに設定されます、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)カプセル化された OID 要求の構造体。

プロトコルのエッジを発行し、 [OID\_切り替える\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)拡張可能スイッチ コントロールのパスをカプセル化された OID 要求を転送するように要求します。 基になる転送拡張機能カプセル化された OID 要求を検査できメンバーが指定したマルチキャスト アドレス情報を保持できます。 たとえば、拡張機能は、拡張可能スイッチ ポートに転送するマルチキャスト パケットが発生した場合にこの情報を必要があります。

拡張可能スイッチの管理パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ コントロール パス](hyper-v-extensible-switch-control-path.md)します。

 

 





