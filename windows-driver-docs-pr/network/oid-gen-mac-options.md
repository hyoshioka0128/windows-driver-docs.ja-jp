---
title: OID_GEN_MAC_OPTIONS
description: クエリとして、OID_GEN_MAC_OPTIONS OID は、基になるドライバーまたは NIC のオプションのプロパティを定義するビットマスクを指定します。
ms.assetid: 2a093bcb-ae6f-491c-a596-03e6f47b0b86
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_MAC_OPTIONS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: e3435c5e38f4196af19ff364a3e6abb8ce947ac4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843073"
---
# <a name="oid_gen_mac_options"></a>OID\_GEN\_MAC\_オプション


クエリとして、OID\_GEN\_MAC\_オプション OID は、基になるドライバーまたは NIC のオプションのプロパティを定義するビットマスクを指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず.

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず.

<a name="remarks"></a>注釈
-------

Ndis は、この OID を NDIS 6.0 以降のミニポートドライバー用に処理します。

このクエリを開始するプロトコルによって、基になるドライバーによって設定されているフラグが決定され、必要に応じてそれらを利用できます。

現在、次のフラグが定義されています。

<a href="" id="ndis-mac-option-copy-lookahead-data"></a>NDIS\_MAC\_オプション\_コピー\_先読み\_データ  
プロトコルドライバーは、指定されたデータに任意の方法でアクセスできます。 一部の高速コピー関数では、オンボードデバイスのメモリにアクセスできません。 マップされたデバイスメモリからデータを示すミニポートドライバーでは、このフラグを設定しないようにしてください。 ミニポートドライバーによってこのフラグが設定されている場合は、高速コピー関数の制限が緩和されます。

<a href="" id="ndis-mac-option-receive-serialized"></a>NDIS\_MAC\_オプション\_シリアル化された\_  
ミニポートドライバーは、パケットをシリアル方式で示します。 つまり、このようなドライバーは、前の受信 (存在する場合) が完了するまで、新しい受信を通知しません。

<a href="" id="ndis-mac-option-transfers-not-pend"></a>NDIS\_MAC\_オプション\_転送\_\_非保留  
ミニポートドライバーは、受信表示を非同期に完了しません。

[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数を使用した受信操作を示すミニポートドライバーは、このフラグを設定する必要があります。

<a href="" id="ndis-mac-option-no-loopback"></a>NDIS\_MAC\_オプション\_\_ループバックなし  
NIC には内部ループバックがサポートされていないため、NDIS はこのドライバーに代わってループバックをを管理します。 ミニポートドライバーは、独自のソフトウェアループバックを NDIS として効率的に提供できないので、NIC でハードウェアループバックがサポートされていない限り、すべてのミニポートドライバーはこのフラグを設定する必要があります。 WAN ミニポートドライバーは、このフラグを設定する必要があります。

<a href="" id="ndis-mac-option-full-duplex"></a>NDIS\_MAC\_オプション\_完全\_二重  
ミニポートドライバーでは、SMP プラットフォームでの全二重の送信とインジケーターがサポートされています。

このフラグは、NDIS 5.0 以降のミニポートドライバーで使用するために非推奨とされ**て  ます**。 NDIS 5.0 以降では、このフラグは無視されます。

 

<a href="" id="ndis-mac-option-eotx-indication"></a>NDIS\_MAC\_オプション\_EOTX\_表示  
このフラグは互換性のために残されています。

<a href="" id="ndis-mac-option-8021p-priority"></a>NDIS\_MAC\_オプション\_8021P\_PRIORITY  
NIC とそのドライバーは、802.1 p パケット優先度をサポートしています。 詳細については、「[パケットの優先順位](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff562331(v=vs.85))」を参照してください。 パケット優先順位の値は、上位層のドライバーから[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体で受信します。 適切な情報は、パケットの MAC ヘッダーに生成され、ネットワーク経由で送信されます。 さらに、この NIC とそのドライバーは、ネットワークから受信したパケットの MAC ヘッダーからの適切な情報の抽出をサポートしています。 この情報は、ネットワーク\_のバッファー構造で上位層のドライバーに転送されます。

  NDIS 6.0 以降およびそれ以降のミニポートドライバーでは、NDIS\_MAC\_オプション\_8021P\_PRIORITY フラグを設定する必要がある**ことに注意**してください。

 

<a href="" id="ndis-mac-option-supports-mac-address-overwrite"></a>NDIS\_MAC\_オプション\_サポート\_MAC\_アドレス\_上書き  
ミニポートドライバーが[**NdisReadNetworkAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadnetworkaddress)関数を呼び出すと、NDIS によってこのフラグが設定されます。

<a href="" id="ndis-mac-option-receive-at-dpc"></a>\_DPC で\_を受信\_NDIS\_MAC\_オプション  
このフラグは互換性のために残されています。

<a href="" id="ndis-mac-option-8021q-vlan"></a>NDIS\_MAC\_オプション\_8021Q\_VLAN  
ミニポートドライバーは、パケットの MAC ヘッダーで VLAN 識別子 (ID) のマーキングを割り当てたり削除したりすることができます。 ドライバーは、ドライバーが処理する各 NIC に対して構成された VLAN ID を保持します。 ドライバーは、NIC が関連付けられている VLAN に属していない着信パケットを除外し、送信パケットを VLAN ID でマークします。 ドライバーの特定の NIC に対する[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数の実行中に、ドライバーは最初に NIC の VLAN ID をゼロに設定します。 次に、ドライバーの*MiniportInitializeEx*関数は、レジストリから次の構成パラメーターを読み取ります。また、パラメーターが存在する場合は、NIC の VLAN ID をパラメーターの値に設定します。

```syntax
VlanId, REG_DWORD
```

<a href="" id="ndis-mac-option-reserved"></a>NDIS\_MAC\_オプション\_予約済み  
NDIS の内部使用のために予約されています。

**注**  NDIS\_MAC\_オプションを設定するミニポートドライバー\_8021Q\_VLAN フラグでは、NDIS\_MAC\_オプション\_8021P\_PRIORITY フラグも設定する必要があります。 言い換えると、802.1 Q をサポートするミニポートドライバーも 802.1 p をサポートする必要があります。

 

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NdisReadNetworkAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadnetworkaddress)

[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)

 

 




