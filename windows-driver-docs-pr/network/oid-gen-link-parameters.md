---
title: OID_GEN_LINK_PARAMETERS
description: セットとして、NDIS およびそれ以降のドライバーは、OID_GEN_LINK_PARAMETERS OID を使用して、ミニポートアダプターの現在のリンクの状態を設定します。 ミニポートドライバーは、NDIS_LINK_PARAMETERS 構造体の双方向の状態、リンク速度、および一時停止の各機能を受け取ります。
ms.assetid: 6a8ee5b1-ac68-424f-b749-45b085ca1d75
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_LINK_PARAMETERS
ms.localizationpriority: medium
ms.openlocfilehash: 7b406886165212a65820260d71f578b6a7e12c29
ms.sourcegitcommit: 3d676aa234debfc34668705beddd36f543f7f828
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86199487"
---
# <a name="oid_gen_link_parameters"></a>OID \_ 生成 \_ リンク \_ パラメーター


セットとして、NDIS およびそれ以降のドライバーは、OID \_ GEN \_ リンクパラメーター oid を使用して、 \_ ミニポートアダプターの現在のリンクの状態を設定します。 ミニポートドライバーは、NDIS \_ リンクパラメーター構造体の双方向の状態、リンク速度、および一時停止の各機能を受け取り \_ ます。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
省略可能。

NDIS \_ リンク \_ パラメーター構造体は、次のように定義されています。

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
NDIS リンクパラメーターの構造体の[**ndis \_ オブジェクト \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)構造体 \_ \_ 。 **ヘッダー**で指定されている構造体の**型**メンバーを ndis オブジェクト型の既定値に設定し、 \_ \_ \_ **リビジョン**メンバーを ndis \_ リンク \_ パラメーター \_ リビジョン1に、 \_ **Size**メンバーを ndis \_ SIZEOF \_ link \_ パラメーター \_ リビジョン \_ 1 に設定します。

<a href="" id="mediaduplexstate"></a>**MediaDuplexState**  
メディアの双方向の状態。 この値は、 [oid の \_ GEN \_ MEDIA \_ DUPLEX \_ 状態](oid-gen-media-duplex-state.md)oid によって返される値と同じです。

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

<a href="" id="ndis-link-state-xmit-link-speed-auto-negotiated"></a>NDIS \_ リンク \_ 状態 \_ XMIT \_ リンク \_ 速度の \_ 自動 \_ ネゴシエート  
アダプターは、リンクパートナーとの間で送信リンク速度を自動ネゴシエートする必要があります。 このフラグが設定されていない場合、ミニポートドライバーは、送信リンク速度を**XmitLinkSpeed**メンバーに指定されている値に設定する必要があります。

<a href="" id="ndis-link-state-rcv-link-speed-auto-negotiated"></a>NDIS \_ リンク \_ 状態 \_ RCV \_ リンク \_ 速度の \_ 自動 \_ ネゴシエート  
アダプターは、リンクパートナーとの間で受信リンク速度を自動ネゴシエートする必要があります。 このフラグが設定されていない場合、ミニポートドライバーは、受信リンク速度を**Rcvlinkspeed**メンバーで指定された値に設定する必要があります。

<a href="" id="ndis-link-state-duplex-auto-negotiated"></a>NDIS \_ リンク \_ 状態 \_ 双方向 \_ 自動 \_ ネゴシエーション  
アダプターは、リンクパートナーと双方向の状態を自動的にネゴシエートする必要があります。 このフラグが設定されていない場合、ミニポートドライバーは、 **MediaDuplexState**メンバーに指定されている値に双方向の状態を設定する必要があります。

<a href="" id="ndis-link-state-pause-functions-auto-negotiated"></a>NDIS \_ リンク \_ 状態の \_ 一時停止 \_ 関数の \_ 自動 \_ ネゴシエート  
ミニポートドライバーは、もう一方の端にある一時停止フレームのサポートを自動ネゴシエートする必要があります。 このフラグが設定されていない場合、ミニポートドライバーは、 **PauseFunctions**メンバーで指定されている pause フレームサポートを使用する必要があります。

<a name="remarks"></a>解説
-------

**メモ** OID 生成 \_ \_ リンク \_ パラメーターを設定すると、接続が失われる可能性があります。 ミニポートドライバーは、この OID が設定されている場合に、ミニポートアダプターを再構成する必要があります。 たとえば、ミニポートドライバーは、既存の接続が失われた場合にミニポートアダプターをリセットできます。 再構成の特定のメカニズムは、アプリケーションに依存します。



OID 生成リンクパラメーターセットの要求のためにミニポートアダプターのリンクの状態が変化した場合 \_ \_ \_ 、ミニポートドライバーは、新しいリンク状態の ndis およびそれ以降のドライバーに通知するために、 [**ndis \_ ステータス \_ リンクの \_ 状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)の状態を示す状態を生成する必要があります。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS \_ オブジェクト \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)

[**NDIS \_ 状態 \_ リンク \_ 状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)

[OID \_ GEN \_ メディア \_ 双方向の \_ 状態](oid-gen-media-duplex-state.md)








