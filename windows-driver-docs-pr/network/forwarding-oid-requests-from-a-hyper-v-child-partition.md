---
title: Hyper-V 子パーティションからの OID 要求の転送
description: Hyper-V 子パーティションからの OID 要求の転送
ms.assetid: 35EA9964-4CD0-4636-9573-65F37393B7E2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90cfdfcb4f95805e5f60cc7487566bef0166b39e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356905"
---
# <a name="forwarding-oid-requests-from-a-hyper-v-child-partition"></a>Hyper-V 子パーティションからの OID 要求の転送


マルチキャストのオブジェクト識別子 (OID) が要求を含む[OID\_802\_3\_追加\_マルチキャスト\_アドレス](https://msdn.microsoft.com/library/windows/hardware/ff569068)と[OID\_802\_3\_削除\_マルチキャスト\_アドレス](https://msdn.microsoft.com/library/windows/hardware/ff569070)関連プロトコルで発行し、ドライバーが次のように動作するをフィルター処理します。

-   HYPER-V 親パーティションで実行されている管理オペレーティング システム。

-   Windows Vista または Windows オペレーティング システムの以降のバージョンを HYPER-V 子パーティションで実行されているゲスト オペレーティング システム。

拡張可能スイッチのインターフェイスは、拡張可能スイッチ コントロール パスにこれらの OID 要求を転送します。 これにより、パーティションで使用されているネットワーク インターフェイスに関する構成情報を取得する拡張機能です。

拡張可能スイッチのプロトコルのエッジがの OID セット要求を転送するなど、 [OID\_802\_3\_追加\_マルチキャスト\_アドレス](https://msdn.microsoft.com/library/windows/hardware/ff569068)ダウン子パーティションから拡張可能スイッチ コントロールのパス。 これにより、そのパーティション内のネットワーク インターフェイスで使用されるマルチキャスト アドレス構成を取得する拡張機能です。

拡張可能スイッチのプロトコルのエッジが内での OID 要求をカプセル化、拡張可能スイッチのインターフェイスでこれらのマルチキャスト OID 要求が届いたら、 [ **NDIS\_切り替える\_NIC\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)構造体。 プロトコルのエッジには、次のようにこの構造体のメンバーも設定します。

-   **SourcePortId**と**SourceNicIndex**メンバーは、OID 要求が発行されたパーティションで使用するポートおよびネットワーク アダプターの対応する値に設定されます。

    **注**  プロトコル エッジが、拡張可能スイッチの内部ネットワーク アダプターの値にこれらのメンバーを設定、マルチキャストの OID 要求は、管理オペレーティング システムから生成されたとき場合、。

     

-   **DestinationPortId**と**DestinationNicIndex**メンバーが 0 に設定します。 これは、カプセル化された OID 要求がコントロール パスの拡張機能に配信されることを指定します。

-   **OidRequest**メンバーのアドレスに設定されます、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)カプセル化された OID 要求の構造体。

プロトコルのエッジを発行し、 [OID\_切り替える\_NIC\_要求](https://msdn.microsoft.com/library/windows/hardware/hh598266)拡張可能スイッチ コントロールのパスをカプセル化された OID 要求を転送するように要求します。 基になる転送拡張機能カプセル化された OID 要求を検査できメンバーが指定したマルチキャスト アドレス情報を保持できます。 たとえば、拡張機能は、拡張可能スイッチ ポートに転送するマルチキャスト パケットが発生した場合にこの情報を必要があります。

拡張可能スイッチの管理パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ コントロール パス](hyper-v-extensible-switch-control-path.md)します。

 

 





