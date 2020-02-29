---
title: OID_GEN_PHYSICAL_MEDIUM
description: クエリとして OID_GEN_PHYSICAL_MEDIUM OID は、NIC がサポートする物理メディアの種類を指定します。
ms.assetid: 84d7231b-8af2-4bdb-8df5-37088767f708
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_PHYSICAL_MEDIUM
ms.localizationpriority: medium
ms.openlocfilehash: 88b5bbb2f2f084994939d95fabc8f557a7f57e3e
ms.sourcegitcommit: 69939496f6d5cb535aad2bd426ab2baa8d7b9051
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78178059"
---
# <a name="oid_gen_physical_medium"></a>OID\_GEN\_物理\_メディア

クエリとして、OID\_GEN\_物理\_MEDIUM OID は、NIC がサポートする物理メディアの種類を指定します。 この OID は、基本的には、[サポートされている\_メディア\_\_GEN](oid-gen-media-supported.md)の拡張機能です。

## <a name="version-information"></a>バージョン情報

**  この**OID は、NDIS 6.0 および6.1 でサポートされています。 NDIS 6.20 以降では、 [OID\_GEN\_物理\_MEDIUM\_EX](oid-gen-physical-medium-ex.md)を使用します。

### <a name="remarks"></a>コメント

NDIS は、この OID をミニポートドライバー用に処理します。 ミニポートドライバーは、初期化中に物理メディアの値を提供します。

ミニポートドライバーは、物理メディアの種類を報告して、 [oid\_GEN\_メディア\_サポート](oid-gen-media-supported.md)対象として宣言したメディアと、サポートされている oid クエリを区別します。 これらのメディアの種類は、次のシステム定義の値の適切なサブセットとして、 **NDIS\_の物理\_中**の列挙型から表示されます。

**NdisPhysicalMediumUnspecified**物理メディアは、上記のメディアのいずれでもありません。 たとえば、一方向のサテライトフィードは、指定されていない物理メディアです。

**NdisPhysicalMediumWirelessLan**802.11 インターフェイスに準拠するミニポートドライバーを使用して、ワイヤレス LAN ネットワーク経由でパケットが転送されます。 このインターフェイスの詳細については、「」を参照してください。 [802.11 ワイヤレス LAN ミニポートドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff543933(v=vs.85))

**NdisPhysicalMediumCableModem**パケットは、DOCSIS ベースのケーブルネットワークを介して転送されます。

**NdisPhysicalMediumPhoneLine**パケットは標準の電話回線を介して転送されます。
たとえば、HomePNA メディアが含まれます。
**NdisPhysicalMediumPowerLine**パケットは、電力分散システムに接続されている配線を介して転送されます。

**NdisPhysicalMediumDSL**パケットは、デジタル加入者線 (DSL) ネットワークを介して転送されます。
たとえば、ADSL や UADSL (-Lite) などが含まれます。
**NdisPhysicalMediumFibreChannel**パケットはファイバーチャネルの相互接続を介して転送されます。

**NdisPhysicalMedium1394**パケットは、IEEE 1394 バスを介して転送されます。

**NdisPhysicalMediumWirelessWan**パケットは、ワイヤレス WAN リンクを介して転送されます。 たとえば、CDPD、CDPD、GPRS などが含まれます。

<a href="" id="ndisphysicalmediumnative802-11"></a>**NdisPhysicalMediumNative802\_11**パケットは、ネイティブ802.11 インターフェイスに準拠するミニポートドライバーを介して、ワイヤレス LAN ネットワークを介して転送されます。 このインターフェイスの詳細については、「[ネイティブ802.11 ワイヤレス LAN ミニポートドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff560648(v=vs.85))」を参照してください。

**  ネイティブ**802.11 インターフェイスは、NDIS 6.0 以降のバージョンでサポートされています。

**NdisPhysicalMediumBluetooth**パケットは、Bluetooth ネットワークを介して転送されます。 Bluetooth は、2.4 GHz のスペクトルを使用する、短い範囲のワイヤレステクノロジです。

**NdisPhysicalMediumInfiniband**Infiniband の物理メディア。 パケットは infiniband の相互接続を介して転送されます。

**NdisPhysicalMediumUWB**Ultra 広域デルファイ法 (UWB) 物理メディア。 パケットは UWB ネットワークを介して転送されます。 UWB は、パーソナルエリアネットワークが高速で短距離間でワイヤレス通信を行うために使用できる無線周波数プラットフォームです。

<a href="" id="ndisphysicalmedium802-3"></a>**NdisPhysicalMedium802\_3**イーサネット (802.3) 物理メディア。 パケットは、802.3 インターフェイス仕様に準拠するミニポートドライバーを介して、ワイヤード (有線) LAN を介して転送されます。 このメディアの種類には、802.3 をエミュレートするデバイスは含まれません。

<a href="" id="ndisphysicalmedium802-5"></a>**NdisPhysicalMedium802\_5**トークンリングの物理メディア。 (802.5 は、NDIS 6.0 以降のドライバーではサポートされていません)。パケットは、802.5 インターフェイス仕様に準拠するミニポートドライバーを介して、トークンリングネットワークを介して転送されます。

**NdisPhysicalMediumIrda**赤外線 (IrDA) 物理メディア。 パケットは、非表示の赤外線光スペクトル (IrDA ネットワーク) を介して転送されます。

**NdisPhysicalMediumWiredWAN**有線、ワイドエリアネットワーク (WAN) の物理メディア。 パケットは、ワイヤード (有線) WAN 経由で転送されます。

**NdisPhysicalMediumWiredCoWan**ワイヤード (接続指向) WAN 物理メディア。 パケットは、接続指向の環境でワイヤード (有線) WAN 経由で転送されます。

**Ndisphys、Mediuマザー**物理メディアは、上記のメディアのいずれでもありません。 **Ndisphysて Mediuマザー**は、NDIS\_物理\_中の列挙に存在しない新しい物理メディアの種類を指定します。

NDIS は、新しいネットワークをサポートするミニポートアダプターに対して、OID\_GEN\_物理\_MEDIUM OID をサポートしています。ただし、これらのネットワークでは、オペレーティングシステムに表示されるパケットと NDIS には、標準および既知のメディアの種類として転送されます。

新しいネットワークでは、標準メディアと同様に表示される可能性のあるパケットが転送されますが、標準とは異なる新しい機能やわずかな違いがある可能性があります。 この OID は、NIC が接続する実際のネットワークを上位層のドライバーとアプリケーションが特定できるように開発されています。 基になるネットワークに関する情報を取得した後、上位層のドライバーとアプリケーションはこの情報を使用して、このようなドライバーやアプリケーションの動作を変更できます。

802.3 NIC と、物理的なメディアの種類が定義されていないエミュレートされた 802.3 NIC を明確に区別するために、NDIS 6.0 以降のバージョンでは、 **NdisPhysicalMedium802\_3**を報告するために802.3 ミニポートドライバーが必要です。

### <a name="requirements"></a>要件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 および6.1 でサポートされています。 NDIS 6.20 以降では、代わりに<a href="oid-gen-physical-medium-ex.md" data-raw-source="[OID_GEN_PHYSICAL_MEDIUM_EX](oid-gen-physical-medium-ex.md)">OID_GEN_PHYSICAL_MEDIUM_EX</a>を使用します。</p></td>
</tr>
<tr class="even">
<td><p>ヘッダー</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>参照

[OID\_GEN\_メディア\_サポートされています](oid-gen-media-supported.md)

[OID\_GEN\_物理\_MEDIUM\_EX](oid-gen-physical-medium-ex.md)
