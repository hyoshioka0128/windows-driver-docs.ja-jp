---
title: OID_WAN_CO_GET_INFO
description: OID_WAN_CO_GET_INFO OID がその NIC 上のすべての仮想接続 (VCs) に適用される情報を返す、ミニポート ドライバーを要求します。 この情報は、次のように定義されている NDIS_WAN_CO_INFO 構造体で返されます。
ms.assetid: c97130a5-68e1-4c69-a5a5-9781ea59af0c
ms.date: 08/08/2017
keywords: -OID_WAN_CO_GET_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: fafc2b348d074a94505dca885aef8100c8387341
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353685"
---
# <a name="oidwancogetinfo"></a>OID\_WAN\_CO\_取得\_情報


OID\_WAN\_CO\_取得\_情報 OID がその NIC 上のすべての仮想接続 (VCs) に適用される情報を返す、ミニポート ドライバーを要求 この情報は、NDIS\_WAN\_CO\_情報構造体の次のように定義されています。

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_INFO {
         OUT ULONG MaxFrameSize;
         OUT ULONG MaxSendWindow;
         OUT ULONG FramingBits;
         OUT ULONG DesiredACCM;
    } NDIS_WAN_CO_INFO, *PNDIS_WAN_CO_INFO;
```




この構造体のメンバーには、次の情報が含まれます。

<a href="" id="maxframesize"></a>**MaxFrameSize**  
ミニポート ドライバーの送信および受信できるネットワーク パケットの最大フレーム サイズを指定します。 この値は、ミニポート ドライバーのフレーム化のオーバーヘッドや PPP HDLC オーバーヘッドを除外する必要があります。 通常この値は約 1500 です。

ただし、すべている CoNDIS WAN ミニポート ドライバーが内部に使用する必要があります**MaxFrameSize**は 32 バイトの返すこの OID 値を超えています。 などをこの OID の 1500 を返している CoNDIS WAN ミニポート ドライバーがそのまま使用内部、および 1532 までを送信する必要があります。 このようなミニポート ドライバーには、将来ブリッジおよびその他のプロトコルに容易をサポートできます。

<a href="" id="maxsendwindow"></a>**MaxSendWindow**  
VC いる CoNDIS WAN ミニポート ドライバーが処理できる未処理のパケットの最大数を指定します。 このメンバーは、少なくとも 1 つに設定する必要があります。

NDISWAN ドライバーが、このメンバーの値を使用しての送信パケットの数に、ミニポート ドライバーの要求を送信するのには制限として*MiniportCoSendPackets* NDISWAN の保留がパケットを送信する前に機能します。 これらのパケットは、ミニポート ドライバーが未処理の送信が完了するまでにキューに登録されます。 動的とを使用して VC あたりごと、ミニポート ドライバーはこの値を調整したり、 **SendWindow**内のメンバー、 [ **WAN\_CO\_LINKPARAMS** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))ミニポート ドライバーに渡します構造[ **NdisMCoIndicateStatus**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553458(v=vs.85))します。 使用して、現在の NDISWAN **SendWindow**として未処理の送信の制限値。 ミニポート ドライバーが設定されている場合**SendWindow** NDISWAN を 0 に特定の VC のパケットの送信を停止する必要があります。 つまり、送信ウィンドウが有効なシャット ダウン、NDISWAN からすべてのパケットを受け付けられないことを指定します、ミニポート ドライバーを指定します。

いる CoNDIS WAN ミニポート ドライバーでは、パケットを内部的には、キューする必要がありますので、値の**MaxSendWindow**理論上は**max**(ULONG)。 ただし、このドライバーにより決定された値は、NIC のリンクの速度、またはハードウェアの機能を反映する必要があります。 たとえば、常に、ミニポート ドライバーの NIC を少なくとも 4 つのパケットのルームの場合、ミニポート ドライバーが設定します**MaxSendWindow** 4 ようにする着信パケット*MiniportCoSendPackets*上に配置できる。すぐのハードウェア。

<a href="" id="framingbits"></a>**FramingBits**  
ミニポート ドライバーではフレームの種類を指定するビットマスクを指定する 32 ビット値。 ミニポート ドライバーでは、バイナリの OR 演算子を使用して、次の値の組み合わせを指定できます。

<a href="" id="ras-framing"></a>RAS\_フレーム  
ミニポート ドライバーが古い RAS フレームを検出できる場合にのみ設定します。 以前の RAS フレームをサポートされているレガシ ドライバーだけでは、このフラグを設定します。

<a href="" id="ras-compression"></a>RAS\_圧縮  
ミニポート ドライバーは、以前の RAS 圧縮スキームをサポートしている場合にのみ設定します。

<a href="" id="ppp-framing"></a>PPP\_フレーム  
常に設定する必要があります。 ミニポート ドライバーを検出し、メディアの種類の PPP フレームをサポートすることを示します。

<a href="" id="ppp-compress-address-control"></a>PPP\_COMPRESS\_ADDRESS\_CONTROL  
ミニポート ドライバーには、PPP アドレスとコントロール フィールドの圧縮がサポートしている場合に設定します。

この LCP オプションがネゴシエートされる場合、NDISWAN はアドレスとコントロールのフィールドを削除します。 X.25 など一部 WAN 中程度の種類では、このオプションをサポートしていません。

<a href="" id="ppp-compress-protocol-field"></a>PPP\_圧縮\_プロトコル\_フィールド  
ミニポート ドライバーには、PPP プロトコル フィールドの圧縮がサポートしている場合に設定します。

NDISWAN はこの LCP オプションがネゴシエートされる場合は、該当する場合は、[プロトコル] フィールドから 1 バイトを削除します。

<a href="" id="ppp-accm-supported"></a>PPP\_ACCM\_サポートされています。  
ミニポート ドライバーは、非同期の制御文字マッピングをサポートしている場合に設定します。 このビットはモデムなどの非同期メディアのみです。 このビットが設定されている場合、 **DesiredACCM**メンバーを有効にする必要があります。

<a href="" id="ppp-multilink-framing"></a>PPP\_マルチリンク\_フレーム  
ミニポート ドライバーは、IETF RFC 1717 で指定されている複数リンク フレームをサポートしている場合に設定します。

<a href="" id="ppp-short-sequence-hdr-format"></a>PPP\_短い\_シーケンス\_HDR\_形式  
ミニポート ドライバーは、IETF RFC 1717 で指定されている複数リンク フレームのヘッダーの形式をサポートしている場合に設定します。

<a href="" id="slip-framing"></a>SLIP\_フレーム  
ミニポート ドライバーを検出し、明細フレーム (非同期のミニポート ドライバーのみ) をサポートする場合に設定します。

<a href="" id="slip-vj-compression"></a>SLIP\_VJ\_COMPRESSION  
明細のミニポート ドライバーが Van Jacobsen TCP/IP ヘッダー圧縮をサポートできる場合に設定します。 NDISWAN サポート スリップ\_VJ\_圧縮 (16 スロット) を使用します。 明細のフレームをサポートする非同期のメディア (シリアル ミニポート ドライバー) は、このビットを設定する必要があります。

非同期のメディアは VJ ヘッダー圧縮をサポートするコードを記述しない必要があります。 NDISWAN は、その考慮されます。

<a href="" id="slip-vj-autodetect"></a>SLIP\_VJ\_AUTODETECT  
場合は、ミニポート ドライバーを自動検出する明細の Van Jacobsen TCP/IP ヘッダー圧縮を設定します。 NDISWAN を自動検出 VJ ヘッダー圧縮します。 非同期のメディア (シリアル ミニポート ドライバー) は、スリップ フレームをサポートしている場合、このビットを設定する必要があります。

<a href="" id="tapi-provider"></a>TAPI\_プロバイダー  
ミニポート ドライバーは、TAPI サービス プロバイダーの Oid をサポートしている場合に設定します。 このビットが設定されていない限り、ミニポート ドライバーに TAPI OID 呼び出しが行わされません。

<a href="" id="media-nrz-encoding"></a>メディア\_NRZ\_エンコード  
ミニポート ドライバーは、エンコード、ISDN など、一部の種類のメディアの PPP 既定 NRZ をサポートしている場合に設定します。 この値は、将来使用するために予約されています。

<a href="" id="media-nrzi-encoding"></a>メディア\_NRZI\_エンコード  
ミニポート ドライバー NRZI エンコードをサポートしている場合に設定します。 この値は、将来使用するために予約されています。

<a href="" id="media-nlpid"></a>メディア\_NLPID  
ミニポート ドライバーがあり、NLPID そのフレームに設定を設定します。 この値は、将来使用するために予約されています。

<a href="" id="rfc-1356-framing"></a>RFC\_1356\_フレーム  
ミニポート ドライバーには、IETF RFC 1356 X.25、ISDN フレームがサポートしている場合に設定します。 この値は、将来使用するために予約されています。

<a href="" id="rfc-1483-framing"></a>RFC\_1483\_FRAMING  
ミニポート ドライバーは、IETF RFC 1483 ATM アダプテーション層 5 カプセル化をサポートしている場合に設定します。 この値は、将来使用するために予約されています。

<a href="" id="rfc-1490-framing"></a>RFC\_1490\_フレーム  
ミニポート ドライバーは、IETF RFC 1490 フレーム リレー フレームをサポートしている場合に設定します。 この値は、将来使用するために予約されています。

<a href="" id="nbf-preserve-mac-address"></a>NBF\_保持\_MAC\_アドレス  
ミニポート ドライバーは、「NETBIOS の PPP フレーム制御プロトコル (NBFCP)」下書きで指定されている、IETF のフレームをサポートしている場合の設定します。

<a href="" id="shiva-framing"></a>SHIVA\_フレーム  
NBF 置き換え\_保持\_MAC\_アドレス。

<a href="" id="pass-through-mode"></a>渡す\_を通じて\_モード  
場合、ミニポート ドライバーは、独自のフレームを設定します。 このフラグが設定されている場合、NDISWAN はフレーム、解釈なしし、未変更の状態を渡します。

各ミニポート ドライバーが受信するまで、ミニポート ドライバーが既定の PPP フレーム モードである必要があります、 [OID\_WAN\_CO\_設定\_リンク\_情報](oid-wan-co-set-link-info.md)要求。 ミニポート ドライバーする必要がありますを自動検出を要求をサポートする任意のフレーム。

たとえば、ミニポート ドライバーを古い RAS フレームをサポートする必要がありますを自動検出 PPP フレームからのフレーミングを RAS。 ミニポート ドライバー検出した場合、既定以外のフレーム化スキーム、ミニポート ドライバーは自動的に新しく検出されたフレームにそのフレームを切り替える必要があります。

後続のクエリで[OID\_WAN\_CO\_取得\_リンク\_情報](oid-wan-co-get-link-info.md)検出されたフレームを指定する必要があります。 フレームがまだ検出されたしない場合、 **FramingBits** NDIS が返された 0 を指定する必要があります\_WAN\_CO\_取得\_リンク\_情報。

OID と WAN ミニポート ドライバーが、その後と呼ばれるかどうか\_WAN\_CO\_設定\_リンク\_情報を**FramingBits**メンバーは 0、ミニポート ドライバー各フレームの受信時にフレームを自動検出を試行する必要があります。

<a href="" id="desiredaccm"></a>**DesiredACCM**  
非同期の制御文字のマップがネゴシエートされます。 このメンバーは、非同期のメディアの種類に対してのみ適用されます。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 および NDIS 5.1 のドライバーを Windows Vista でサポートされています。 Windows XP で 5.1 の NDIS ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NdisMCoIndicateStatus**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553458(v=vs.85))

[OID\_WAN\_CO\_取得\_リンク\_情報](oid-wan-co-get-link-info.md)

[OID\_WAN\_CO\_SET\_LINK\_INFO](oid-wan-co-set-link-info.md)

[**WAN\_CO\_LINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))








