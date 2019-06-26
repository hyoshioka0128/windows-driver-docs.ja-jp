---
title: コネクションレス ミニポート ドライバーのクエリ
description: コネクションレス ミニポート ドライバーのクエリ
ms.assetid: a556d7ba-52ea-443b-994b-4c517e80ac55
keywords:
- コネクションレス ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45570e93eb520794ea3ae490116b3401c0033e6c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385443"
---
# <a name="querying-a-connectionless-miniport-driver"></a>コネクションレス ミニポート ドライバーのクエリ





バインドされているプロトコルを呼び出すコネクションレス ミニポート ドライバーを保持する Oid を照会する[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)渡します、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造を照会して、NDIS 最終的に情報を書き込みます、要求されたバッファーを指すオブジェクト (OID) を指定します。

NDIS ミニポート ドライバーへの呼び出しに応答しないかどうか**NdisOidRequest** NDIS ミニポート ドライバーを呼び出すと、 [ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)を返す関数NDIS に必要な情報。 *MiniportOidRequest*への呼び出しでの同期または非同期で完了できます[ **NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)します。

NDIS ミニポート ドライバーを呼び出すことも*MiniportOidRequest*ミニポート ドライバーの後に、自身が代理として--で機能*MiniportInitializeEx*関数が NDIS を返しました\_ステータス\_成功--ミニポート ドライバーの機能、状態、または統計情報を照会します。 次の図は、コネクションレス ミニポート ドライバーにクエリを実行します。

![コネクションレスのミニポート ドライバーのクエリを実行するかを示す図](images/fig5-2.png)

NDIS は、ミニポート ドライバーの代わりに多くの OID 要求に応答します。 状態インジケーターで、初期化中に多くの OID 値のミニポート ドライバーを報告します。 属性で報告される OID 値の詳細については、次を参照してください[ **NDIS\_ミニポート\_アダプター\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_attributes)と関連する属性。構造体。

ときに*MiniportOidRequest* OID を使用して呼び出した\_GEN\_MAC\_オプション、ミニポート ドライバーを実行する省略可能な操作を指定するビットマスクを返す必要があります。 フラグのセットが含まれます。

-   NDIS\_MAC\_オプション\_コピー\_先読み\_データ。 このフラグは、任意の方法で指定されたデータにアクセスできることにプロトコル ドライバーを示します。 ミニポート ドライバーでは、オンボードの共有メモリからデータを示します場合、このフラグは設定する必要があります。

-   NDIS\_MAC\_オプション\_いいえ\_ループバックします。 このフラグを設定するとに渡されるパケットにミニポート ドライバーがないループバック*MiniportSendNetBufferLists(Packets)* は同じコンピューター上の受信者に送られますが、およびミニポート ドライバーを実行する NDIS が必要ですが、ループバックします。 NDIS は、パケットのループバックを実行する場合、パケットは渡されませんミニポート ドライバーに。 ミニポート ドライバーは、NIC がハードウェア ループバックを実行しない限り、常にこのフラグを設定します。

-   NDIS\_MAC\_オプション\_受信\_シリアル化します。 このフラグが設定されている場合、ミニポート ドライバーには、以前に受信したパケットが完全に処理されたなどのデータを転送するまで新しくパケットを受信いずれかは示されません。 ほとんどのミニポート ドライバーを除く、パケットを呼び出すことによって示す[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)、このフラグを設定します。

ミニポート ドライバーは、NDIS フラグを使用しないでください必要があります\_MAC\_オプション\_NDIS 内部使用用に予約された予約されています。

*MiniportOidRequest*は、NIC の現在のアドレスを決定するメディア固有の OID でもクエリを実行します。 OID での型 802.3 の NIC のミニポート ドライバーの照会、\_802\_3\_現在\_アドレス。

メディアに固有である追加の Oid は、特定のメディア タイプのミニポート ドライバーが表示されます。 OID での NIC が型 802.3 ミニポート ドライバーを照会するなど、\_802.3\_最大\_一覧\_サイズ。 詳細については、次を参照してください。[全般オブジェクト](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))します。

 

 





