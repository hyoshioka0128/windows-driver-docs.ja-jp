---
title: OID_GEN_LINK_PARAMETERS
description: セットとして NDIS および上にあるドライバーはミニポート アダプターの現在のリンク状態を設定するのに OID_GEN_LINK_PARAMETERS OID を使用します。 ミニポート ドライバーでは、NDIS_LINK_PARAMETERS 構造体で双方向の状態、リンク速度、および一時停止の関数を受け取ります。
ms.assetid: 6a8ee5b1-ac68-424f-b749-45b085ca1d75
ms.date: 08/08/2017
keywords: -OID_GEN_LINK_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1d4ddf0d0f5a3132cf6365dc1edd8a17e142a92f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369102"
---
# <a name="oidgenlinkparameters"></a>OID\_GEN\_リンク\_パラメーター


セットとして NDIS と関連付けたドライバー使用 OID\_GEN\_リンク\_ミニポート アダプターの現在のリンク状態を設定するパラメーターの OID。 ミニポート ドライバーでは、NDIS で双方向の状態、リンク速度、および一時停止機能が受信\_リンク\_パラメーター構造体。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
必須。

NDIS\_リンク\_パラメーター構造は次のように定義されます。

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




この構造体には、次のメンバーが含まれています。

<a href="" id="header"></a>**ヘッダー**  
[ **NDIS\_オブジェクト\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header) NDIS 構造\_リンク\_パラメーター構造体。 設定、**型**、構造体のメンバーを**ヘッダー**を使用する NDIS\_オブジェクト\_型\_既定では、**リビジョン**NDIS メンバー\_リンク\_パラメーター\_リビジョン\_1、および**サイズ**NDIS メンバー\_SIZEOF\_リンク\_パラメーター\_リビジョン\_1。

<a href="" id="mediaduplexstate"></a>**MediaDuplexState**  
メディアの双方向状態。 この値は、によって返される値と同じ、 [OID\_GEN\_メディア\_双方向\_状態](oid-gen-media-duplex-state.md)OID。

<a href="" id="xmitlinkspeed"></a>**XmitLinkSpeed**  
1 秒あたりのビット単位で送信リンク速度。

<a href="" id="rcvlinkspeed"></a>**RcvLinkSpeed**  
1 秒あたりのビット単位の受信リンク速度。

<a href="" id="pausefunctions"></a>**PauseFunctions**  
IEEE 802.3 pause フレームのサポートの種類。 このメンバーは、次の一時停止機能の 1 つを指定する必要があります。

<a href="" id="ndispausefunctionsunsupported"></a>**NdisPauseFunctionsUnsupported**  
アダプターまたはリンクのパートナーは、一時停止のフレームをサポートしていません。

<a href="" id="ndispausefunctionssendonly"></a>**NdisPauseFunctionsSendOnly**  
アダプターとリンク パートナー サポートのみ一時停止のフレームをアダプターからリンク パートナーに送信します。

<a href="" id="ndispausefunctionsreceiveonly"></a>**NdisPauseFunctionsReceiveOnly**  
のみ一時停止のフレームをリンクのパートナーからアダプターに送信アダプターとリンク パートナーのサポート

<a href="" id="ndispausefunctionssendandreceive"></a>**NdisPauseFunctionsSendAndReceive**  
アダプターとリンク パートナーは、送信し、方向の受信の両方でフレームを一時停止を送受信することをサポートします。

<a href="" id="autonegotiationflags"></a>**AutoNegotiationFlags**  
ミニポート アダプターの自動ネゴシエーション設定します。 このメンバーは、次のフラグのビットごとの OR から作成されます。

<a href="" id="ndis-link-state-xmit-link-speed-auto-negotiated"></a>NDIS\_リンク\_状態\_XMIT\_リンク\_速度\_自動\_NEGOTIATED  
アダプターは自動ネゴシエーション送信リンクの速度リンク パートナーと。 ミニポート ドライバーがで指定されている値に送信リンクの速度を設定する必要がありますこのフラグが設定されていない場合、 **XmitLinkSpeed**メンバー。

<a href="" id="ndis-link-state-rcv-link-speed-auto-negotiated"></a>NDIS\_リンク\_状態\_受信\_リンク\_速度\_自動\_NEGOTIATED  
アダプターが自動ネゴシエーション受信リンクの速度リンク パートナーと。 ミニポート ドライバーがで指定されている値に受信リンクの速度を設定する必要がありますこのフラグが設定されていない場合、 **RcvLinkSpeed**メンバー。

<a href="" id="ndis-link-state-duplex-auto-negotiated"></a>NDIS\_リンク\_状態\_双方向\_自動\_NEGOTIATED  
アダプターが自動ネゴシエーションが双方向の状態リンク パートナーと。 ミニポート ドライバーがで指定されている値に双方向の状態を設定する必要がありますこのフラグが設定されていない場合、 **MediaDuplexState**メンバー。

<a href="" id="ndis-link-state-pause-functions-auto-negotiated"></a>NDIS\_リンク\_状態\_一時停止\_関数\_自動\_NEGOTIATED  
ミニポート ドライバーが自動ネゴシエーションもう一方の end で一時停止のフレームのサポート。 ミニポート ドライバーがで指定されている一時停止のフレームのサポートを使用する必要がありますこのフラグが設定されていない場合、 **PauseFunctions**メンバー。

<a name="remarks"></a>注釈
-------

**注**設定 OID\_GEN\_リンク\_パラメーター接続の損失が発生することができます。 この OID が設定されている場合に、ミニポート ドライバーはミニポート アダプターを再構成する必要があります。 たとえば、ミニポート ドライバーでは、ミニポート アダプターの既存の接続が失われるとをリセットできます。 再構成の特定のメカニズムは、アプリケーションに依存します。



OID のためのミニポート アダプターのリンクの状態が変更された場合\_GEN\_リンク\_パラメーターが要求を設定、ミニポート ドライバーを生成する必要があります、 [ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state) NDIS と新しいリンクの状態の上にあるドライバーを通知する状態を示す値。

<a name="requirements"></a>必要条件
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


[**NDIS\_オブジェクト\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)

[**NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)

[OID\_GEN\_メディア\_双方向\_状態](oid-gen-media-duplex-state.md)








