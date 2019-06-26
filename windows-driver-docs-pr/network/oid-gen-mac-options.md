---
title: OID_GEN_MAC_OPTIONS
description: OID_GEN_MAC_OPTIONS OID として、クエリには、基になるドライバーまたは NIC の省略可能なプロパティを定義するビットマスクを指定します
ms.assetid: 2a093bcb-ae6f-491c-a596-03e6f47b0b86
ms.date: 08/08/2017
keywords: -OID_GEN_MAC_OPTIONS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4bd0808748c52707354155a052c832c2e51b8ea9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369058"
---
# <a name="oidgenmacoptions"></a>OID\_GEN\_MAC\_オプション


クエリ、OID として\_GEN\_MAC\_オプション OID を基になるドライバーまたは NIC の省略可能なプロパティを定義するビットマスクを指定します

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

NDIS は、NDIS 6.0 とそれ以降のミニポート ドライバーのこの OID を処理します。

A プロトコルのが開始され次のクエリを調べるフラグの基になるドライバーの設定、およびそれらのオプションで利用できます。

次のフラグは現在定義されています。

<a href="" id="ndis-mac-option-copy-lookahead-data"></a>NDIS\_MAC\_オプション\_コピー\_先読み\_データ  
プロトコル ドライバーには任意の方法で指定されたデータにアクセスできます。 一部の高速コピー関数では、オンボード デバイス メモリへのアクセスに問題があります。 マップされているデバイスのメモリ不足データを示す、ミニポート ドライバーでは、このフラグは設定しないでください必要があります。 ミニポート ドライバーはこのフラグを設定する場合は、fast コピー関数の制限を緩和します。

<a href="" id="ndis-mac-option-receive-serialized"></a>NDIS\_MAC\_オプション\_受信\_シリアル化  
ミニポート ドライバーでは、順番にパケットを示します。 つまり、このようなドライバーが入力されていない新しい、いずれかが完了した場合は、前の受信までを示す値を受信します。

<a href="" id="ndis-mac-option-transfers-not-pend"></a>NDIS\_MAC\_オプション\_転送\_いない\_保留  
ミニポート ドライバーが完了しない問題を非同期的に受信します。

示すミニポート ドライバーでの操作の受信、 [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数は、このフラグを設定する必要があります。

<a href="" id="ndis-mac-option-no-loopback"></a>NDIS\_MAC\_オプション\_いいえ\_ループバック  
NDIS は、このドライバーに代わってループバックするを管理するため、NIC は内部のループバックのサポートがありません。 NIC にハードウェア ループバックのサポートがない限り、すべてのミニポート ドライバーでこのフラグを設定する必要がありますので、ミニポート ドライバーは、独自のソフトウェアのループバックを NDIS、として効率的に提供できません。 WAN ミニポート ドライバーでは、このフラグを設定する必要があります。

<a href="" id="ndis-mac-option-full-duplex"></a>NDIS\_MAC\_オプション\_完全\_双方向  
ミニポート ドライバーがサポートする完全な双方向の送信と SMP のプラットフォームで表示します。

**注**  NDIS 5.0 およびそれ以降のミニポート ドライバーで使用するためこのフラグは非推奨です。 NDIS 5.0 以降では、このフラグは無視されます。

 

<a href="" id="ndis-mac-option-eotx-indication"></a>NDIS\_MAC\_オプション\_EOTX\_を示す値  
このフラグは廃止されています。

<a href="" id="ndis-mac-option-8021p-priority"></a>NDIS\_MAC\_オプション\_8021 P\_優先順位  
NIC とそのドライバーは、802.1 p のパケットの優先順位をサポートします。 詳細については、次を参照してください。[パケットの優先順位](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff562331(v=vs.85))します。 パケットの優先度の値がで受信した[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)上位レイヤー ドライバーからの構造体。 適切な情報がパケットの MAC ヘッダーで生成され、ネットワーク経由で送信します。 さらに、この NIC とそのドライバーは、ネットワークから受信したパケットの MAC ヘッダーから適切な情報の抽出をサポートします。 NET でこの情報が転送される\_上位層のドライバーにバッファーの構造体。

**注**  NDIS 6.0 と以降およびそれ以降、およびそれ以降のミニポート ドライバーは、NDIS を設定する必要があります\_MAC\_オプション\_8021 P\_優先順位フラグ。

 

<a href="" id="ndis-mac-option-supports-mac-address-overwrite"></a>NDIS\_MAC\_オプション\_サポート\_MAC\_アドレス\_上書き  
NDIS は、ミニポート ドライバーを呼び出すときにこのフラグを設定、 [ **NdisReadNetworkAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadnetworkaddress)関数。

<a href="" id="ndis-mac-option-receive-at-dpc"></a>NDIS\_MAC\_オプション\_受信\_で\_DPC  
このフラグは廃止されています。

<a href="" id="ndis-mac-option-8021q-vlan"></a>NDIS\_MAC\_オプション\_8021Q\_VLAN  
ミニポート ドライバーでは、割り当てるでき、パケットの MAC ヘッダーで VLAN 識別子 (ID) マーキングを削除することができます。 ドライバーは、ドライバーを処理する各 NIC の構成済みの VLAN ID を保持します。 受信パケットを NIC が関連付けられているし、VLAN ID を持つ送信パケットをマークの VLAN に属していないドライバーをフィルター処理します。 ドライバーの中に[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)特定の NIC ドライバーの関数が最初に、NIC の VLAN ID を 0 に設定します。 ドライバーの*MiniportInitializeEx*関数し、レジストリから次の構成パラメーターを読み取るし、パラメーターが存在する場合は、NIC の VLAN ID をパラメーターの値に設定します。

```syntax
VlanId, REG_DWORD
```

<a href="" id="ndis-mac-option-reserved"></a>NDIS\_MAC\_オプション\_予約済み  
NDIS 内部使用のために予約されています。

**注**  設定、NDIS ミニポート ドライバー\_MAC\_オプション\_8021Q\_VLAN フラグは、NDIS を設定する必要がありますも\_MAC\_オプション\_8021 P\_優先順位フラグ。 つまり、802.1 q をサポートしているミニポート ドライバーは、802.1 p もサポートする必要があります。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)

[**NdisReadNetworkAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadnetworkaddress)

[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)

 

 




