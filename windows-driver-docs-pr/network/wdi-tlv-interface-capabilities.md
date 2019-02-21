---
title: WDI_TLV_INTERFACE_CAPABILITIES
description: WDI_TLV_INTERFACE_CAPABILITIES では、Wi-fi インターフェイスの機能を含む TLV です。
ms.assetid: 308331DD-FEEB-4C49-BEBD-117AE58D4792
ms.date: 07/18/2017
keywords:
- WDI_TLV_INTERFACE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5482be969dd2b31106647416c4a847a5ae6ba480
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531479"
---
# <a name="wditlvinterfacecapabilities"></a>WDI\_TLV\_インターフェイス\_機能


WDI\_TLV\_インターフェイス\_機能は、Wi-fi インターフェイスの機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0 xf です.

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


Uint32 型の説明を入力、最大転送単位 (MTU) のサイズ。
UINT32 アダプターのマルチキャスト リスト サイズ。
UINT16 (バイト単位) バックフィル サイズ。 この値は 256 バイトより大きくすることはできません。
[**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)アダプターの永続的な MAC アドレス。 デバイスは、複数の永続的な MAC アドレスをサポートする場合は、デバイスによって使用される最初の MAC アドレスが返されます。
UINT32 と、サポートされている最大送信速度を (kbps) には、このアダプター。
UINT32 kbps で、サポートされている最大がこのアダプターのレートを受信します。
UINT8 は、ハードウェアによってオプションが有効になっているかどうかを指定します。 有効な値は 0 (無効) および 1 (有効です)。
UINT8 は、ソフトウェアで有効になってがオプションかどうかを指定します。 有効な値は 0 (無効) および 1 (有効です)。
UINT8 はするが、インターフェイスにサポートしているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。
UINT8 は、インターフェイスが FLR をサポートしているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。
UINT8 は、アクションのフレームを送受信することはサポートされているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。
UINT8 RX の空間ストリームのサポートされている数。
UINT8 TX 空間ストリームのサポートされている数。
UINT8、アダプター同時に作業できる、操作モードに関係なくチャネルの数。
UINT8 は、アンテナの多様性がサポートされているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。
UINT8 は eCSA がサポートされているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。
UINT8 は、アダプターが MAC アドレスのランダム化をサポートしているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。
[**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)ビット マスク アドレスができるかどうかのビットごとのランダム化された (0) を指定する、または永続的なアドレス (1) と同じ値を保持する必要があります。 既定値はすべて 0 になります。
[**WDI\_BLUETOOTH\_共存\_サポート**](https://msdn.microsoft.com/library/windows/hardware/dn897795) (UINT32) - Wi-fi、Bluetooth の共存のサポートされているレベル。
WDI 以外の OID のサポートの UINT8 を指定します。 有効な値は次のとおりです。
-   0 :サポートされません。 Microsoft コンポーネントは、アダプターに転送されていないを理解していない Oid。
-   1 :サポートされています。 Microsoft コンポーネントは、アダプターに転送されますを理解していない Oid。

これらの Oid には、WDI ヘッダーは含まれません。 要求を受信したアダプターのポートを識別するために、ndis NdisPortNumber を使用して、\_OID\_要求との照合[WDI\_タスク\_作成\_ポート](https://msdn.microsoft.com/library/windows/hardware/dn925949).

UINT8 は、高速の移行がサポートされているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。
UINT8 は Mu MIMO がサポートされているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。
UINT8 は、インターフェイスは、Miracast シンクをサポートできない場合を指定します。 有効な値は 0 (サポート) および 1 (サポートされていませんです)。
UINT8 指定場合 802.11v BSS 移行がサポートされています。 有効な値は 0 (サポートされていません) および 1 (サポートです)。
UINT8

Windows 10 version 1607 では、バージョン 1.0.21 WDI に追加されます。

デバイスがドッキング機能 IP をサポートしているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。
 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




