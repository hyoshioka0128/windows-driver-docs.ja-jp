---
title: OID_GEN_PHYSICAL_MEDIUM
description: クエリとして OID_GEN_PHYSICAL_MEDIUM OID には、NIC をサポートする物理メディアの種類を指定します。
ms.assetid: 84d7231b-8af2-4bdb-8df5-37088767f708
ms.date: 08/08/2017
keywords: -OID_GEN_PHYSICAL_MEDIUM ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5627c37f1bef00ea906d4fa5f46f932898a6604b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560345"
---
# <a name="oidgenphysicalmedium"></a>OID\_GEN\_物理\_中


クエリ、OID として\_GEN\_物理\_MEDIUM OID は、NIC をサポートする物理メディアの種類を指定します。 この OID の拡張機能では基本的には、 [OID\_GEN\_メディア\_サポートされている](oid-gen-media-supported.md)します。

**バージョン情報**

**注**  NDIS 6.0 および 6.1 でこの OID がサポートされています。 NDIS 6.20 以降を使用して[OID\_GEN\_物理\_MEDIUM\_EX](oid-gen-physical-medium-ex.md)します。

 

<a name="remarks"></a>注釈
-------

NDIS は、ミニポート ドライバーには、この OID を処理します。 ミニポート ドライバーでは、初期化中に物理中程度の値を提供します。

ミニポート ドライバーでサポートするために宣言されているメディアから、物理メディアを区別するために、物理メディアの種類のレポート、 [OID\_GEN\_メディア\_サポートされている](oid-gen-media-supported.md)OID クエリ。 メディアの種類は、次のシステム定義値からの適切なサブセットとして一覧表示されます、 **NDIS\_物理\_MEDIUM**列挙体。

**NdisPhysicalMediumUnspecified**物理メディアは、前のメディアなし。 たとえば、一方向のサテライト フィードは、指定されていない物理メディアです。

**NdisPhysicalMediumWirelessLan** 802.11 インターフェイスに準拠しているミニポート ドライバーを通じてワイヤレス LAN ネットワーク経由でパケットが転送されます。 このインターフェイスの詳細についてを参照してください。 [802.11 ワイヤレス LAN のミニポート ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff543933)

**NdisPhysicalMediumCableModem** DOCSIS ベース ケーブルのネットワークを介してパケットが転送されます。

**NdisPhysicalMediumPhoneLine**標準の電話回線を介してパケットが転送されます。
たとえば、HomePNA メディアが含まれます。
**NdisPhysicalMediumPowerLine**配布システムの電源に接続されている接続を介してパケットが転送されます。

**NdisPhysicalMediumDSL**デジタル加入者線 (DSL) ネットワークを介してパケットが転送されます。
たとえば、ADSL、UADSL (G.Lite) に含まれています。
**NdisPhysicalMediumFibreChannel**ファイバー チャネルの相互接続を介してパケットが転送されます。

**NdisPhysicalMedium1394**パケットは、IEEE 1394 バス経由で転送されます。

**NdisPhysicalMediumWirelessWan**ワイヤレス WAN リンク経由でパケットが転送されます。 たとえば、CDPD、CDMA、および GPRS に含まれています。

<a href="" id="ndisphysicalmediumnative802-11"></a>**NdisPhysicalMediumNative802\_11**ネイティブ 802.11 インターフェイスに準拠のミニポート ドライバーを介してワイヤレス LAN ネットワーク経由でパケットが転送されます。 このインターフェイスの詳細については、[802.11 ワイヤレス LAN のネイティブのミニポート ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff560648)を参照してください。

**注**  NDIS 6.0 以降およびそれ以降、およびそれ以降のバージョンで、ネイティブの 802.11 インターフェイスがサポートされています。

 

**NdisPhysicalMediumBluetooth** Bluetooth ネットワークを介してパケットが転送されます。 Bluetooth は、2.4 GHz のスペクトルを使用する近距離ワイヤレス テクノロジです。

**NdisPhysicalMediumInfiniband** Infiniband 物理メディア。 Infiniband 相互接続を通じてパケットが転送されます。

**NdisPhysicalMediumUWB** Ultra 広域デルファイ (UWB) 物理メディア。 UWB ネットワーク経由でパケットが転送されます。 UWB は、パーソナル エリア ネットワークは、高速で近距離無線通信に使用できるを無線周波数プラットフォームです。

<a href="" id="ndisphysicalmedium802-3"></a>**NdisPhysicalMedium802\_3**物理メディアをイーサネット (802.3)。 パケットは、802.3 インターフェイスの仕様に準拠しているミニポート ドライバーを介してワイヤード (有線) LAN 経由で転送されます。 このメディアの種類では、802.3 をエミュレートするデバイスは含まれません。

<a href="" id="ndisphysicalmedium802-5"></a>**NdisPhysicalMedium802\_5**トークン リングの物理メディア。 (802.5 は NDIS 6.0 とそれ以降およびそれ以降のドライバーでないサポート)。パケットは、802.5 インターフェイスの仕様に準拠しているミニポート ドライバーを通じてトークン リング ネットワーク経由で転送されます。

**NdisPhysicalMediumIrda**赤外線 (IrDA) 物理メディア。 パケットは、ライト スペクトルが表示されない、赤外線 IrDA ネットワーク経由で転送されます。

**NdisPhysicalMediumWiredWAN**ワイヤード (有線)、ワイド エリア ネットワーク (WAN) の物理メディア。 パケットは、ワイヤード (有線)、WAN 経由で転送されます。

**NdisPhysicalMediumWiredCoWan**ワイヤード (有線)、接続指向の WAN 物理メディア。 パケットは、接続指向の環境でのワイヤード (有線)、WAN 経由で転送されます。

**NdisPhysicalMediumOther**物理メディアは、前のメディアなし。 **NdisPhysicalMediumOther**指定、新しい物理メディアの種類には、NDIS に存在しません\_物理\_中程度の列挙体。

NDIS サポート、OID\_GEN\_物理\_ミニポート アダプターがこれらのネットワーク、オペレーティング システムと標準と既知の NDIS に表示されているパケットを転送する場合でも、新しいネットワークをサポートするための媒体 OIDメディアの種類。

新しいネットワークでは、標準のメディアのように表示される可能性がありますが、新しい機能や、標準のわずかな違いがある可能性がありますのパケットを転送します。 上位層のためのドライバーが開発されたこの OID と、アプリケーションは、NIC が接続する実際のネットワークを判断できます。 基になるネットワークに関する情報を取得するには、後に上位層のドライバーとアプリケーションはこのようなドライバーとアプリケーションの動作を変更するのにこの情報を使用できます。

NIC はありませんし、定義されている物理メディアの種類、NDIS 6.0 以降およびそれ以降、およびそれ以降のバージョン、エミュレートされた 802.3 から 802.3 の NIC を明確に区別するためにレポートを 802.3 ミニポート ドライバーを必要と**NdisPhysicalMedium802\_3**.

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 および 6.1 ではサポートされています。 NDIS 6.20 以降を使用して<a href="oid-gen-physical-medium-ex.md" data-raw-source="[OID_GEN_PHYSICAL_MEDIUM_EX](oid-gen-physical-medium-ex.md)">OID_GEN_PHYSICAL_MEDIUM_EX</a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_GEN\_メディア\_サポートされています。](oid-gen-media-supported.md)

[OID\_GEN\_物理\_MEDIUM\_例](oid-gen-physical-medium-ex.md)

 

 




