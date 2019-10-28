---
title: OID_GEN_LINK_PARAMETERS
description: セットとして、NDIS およびそれ以降のドライバーは、OID_GEN_LINK_PARAMETERS OID を使用して、ミニポートアダプターの現在のリンクの状態を設定します。 ミニポートドライバーは、NDIS_LINK_PARAMETERS 構造体の双方向の状態、リンク速度、および一時停止の各機能を受け取ります。
ms.assetid: 6a8ee5b1-ac68-424f-b749-45b085ca1d75
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_LINK_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 9c100faed784a0bbb121aacbce077ef120862cc4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843072"
---
# <a name="oid_gen_link_parameters"></a>OID\_GEN\_LINK\_パラメーター


セットとして、NDIS およびそれ以降のドライバーは OID\_GEN\_リンク\_PARAMETERS OID を使用して、ミニポートアダプターの現在のリンクの状態を設定します。 ミニポートドライバーは、NDIS\_リンク\_PARAMETERS 構造体の双方向の状態、リンク速度、および一時停止の各機能を受け取ります。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
必ず.

NDIS\_LINK\_PARAMETERS 構造体は、次のように定義されています。

```ManagedCPlusPlus
    typedef struct _NDIS_LINK_PARAMETERS {
         NDIS_OBJECT_HEADER Header;
         NDIS_MEDIA_DUPLEX_STATE MediaDuplexState;
         ULONG64 XmitLinkSpeed;
         ULONG64 RcvLinkSpeed;
         NDIS_SUPPORTED_PAUSE_FUNCTIONS PauseFunctions;
         ULONG AutoNegotiationFlags;
    } NDIS_LINK_PARAMETERS, *PNDIS_LINK_PARAMETERS;
```




この構造体には、次のメンバーが含まれます。

<a href="" id="header"></a>**項目**  
Ndis [ **\_オブジェクト\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header) 、NDIS\_LINK\_PARAMETERS 構造体のヘッダー構造です。 **ヘッダー**で指定されている構造体の**型**メンバーを ndis\_オブジェクトに設定します\_Type\_DEFAULT、 **REVISION**メンバーを NDIS\_LINK\_\_のリビジョン\_1、および**サイズ**メンバーを NDIS\_SIZEOF\_\_パラメーター\_リビジョン\_1 にリンクします。

<a href="" id="mediaduplexstate"></a>**MediaDuplexState**  
メディアの双方向の状態。 この値は、 [oid\_GEN\_MEDIA\_DUPLEX\_状態](oid-gen-media-duplex-state.md)oid によって返される値と同じです。

<a href="" id="xmitlinkspeed"></a>**XmitLinkSpeed**  
送信リンク速度 (ビット/秒)。

<a href="" id="rcvlinkspeed"></a>**RcvLinkSpeed**  
受信リンク速度 (ビット/秒)。

<a href="" id="pausefunctions"></a>**PauseFunctions**  
IEEE 802.3 の一時停止フレームのサポートの種類。 このメンバーは、次の一時停止関数のいずれかである必要があります。

<a href="" id="ndispausefunctionsunsupported"></a>**Ndispauseモジュールはサポートされていません**  
アダプターまたはリンクパートナーは、一時停止フレームをサポートしていません。

<a href="" id="ndispausefunctionssendonly"></a>**NdisPauseFunctionsSendOnly**  
アダプターおよびリンクパートナーは、アダプターからリンクパートナーへの一時停止フレームの送信のみをサポートしています。

<a href="" id="ndispausefunctionsreceiveonly"></a>**Ndispauseモジュール Receiveonly**  
アダプターおよびリンクパートナーは、リンクパートナーからアダプターへの一時停止フレームの送信のみをサポートしています。

<a href="" id="ndispausefunctionssendandreceive"></a>**NdisPauseFunctionsSendAndReceive**  
アダプターおよびリンクパートナーは、送信と受信の両方向の一時停止フレームの送受信をサポートしています。

<a href="" id="autonegotiationflags"></a>**AutoNegotiationFlags**  
ミニポートアダプターの自動ネゴシエーション設定。 このメンバーは、次のフラグのビットごとの OR から作成されます。

<a href="" id="ndis-link-state-xmit-link-speed-auto-negotiated"></a>NDIS\_LINK\_STATE\_XMIT\_LINK\_自動\_ネゴシエートされる\_  
アダプターは、リンクパートナーとの間で送信リンク速度を自動ネゴシエートする必要があります。 このフラグが設定されていない場合、ミニポートドライバーは、送信リンク速度を**XmitLinkSpeed**メンバーに指定されている値に設定する必要があります。

<a href="" id="ndis-link-state-rcv-link-speed-auto-negotiated"></a>NDIS\_LINK\_STATE\_RCV\_LINK\_AUTO\_ネゴシエート  
アダプターは、リンクパートナーとの間で受信リンク速度を自動ネゴシエートする必要があります。 このフラグが設定されていない場合、ミニポートドライバーは、受信リンク速度を**Rcvlinkspeed**メンバーで指定された値に設定する必要があります。

<a href="" id="ndis-link-state-duplex-auto-negotiated"></a>NDIS\_リンク\_状態\_双方向\_自動\_ネゴシエートされる  
アダプターは、リンクパートナーと双方向の状態を自動的にネゴシエートする必要があります。 このフラグが設定されていない場合、ミニポートドライバーは、 **MediaDuplexState**メンバーに指定されている値に双方向の状態を設定する必要があります。

<a href="" id="ndis-link-state-pause-functions-auto-negotiated"></a>NDIS\_リンク\_状態\_自動\_ネゴシエートさ\_\_関数を一時停止します。  
ミニポートドライバーは、もう一方の端にある一時停止フレームのサポートを自動ネゴシエートする必要があります。 このフラグが設定されていない場合、ミニポートドライバーは、 **PauseFunctions**メンバーで指定されている pause フレームサポートを使用する必要があります。

<a name="remarks"></a>注釈
-------

**メモ** OID\_GEN\_LINK\_パラメーターを設定すると、接続が失われる可能性があります。 ミニポートドライバーは、この OID が設定されている場合に、ミニポートアダプターを再構成する必要があります。 たとえば、ミニポートドライバーは、既存の接続が失われた場合にミニポートアダプターをリセットできます。 再構成の特定のメカニズムは、アプリケーションに依存します。



OID\_GEN\_LINK\_PARAMETERS set request のために、ミニポートアダプターのリンクの状態が変化した場合、ミニポートドライバーは、通知を行うために\_状態の状態を示す[ **\_リンクを\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)生成する必要があります。新しいリンク状態の NDIS およびそれ以降のドライバー。

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


[**NDIS\_オブジェクト\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)

[**NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)

[OID\_GEN\_メディア\_双方向\_状態](oid-gen-media-duplex-state.md)








