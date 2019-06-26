---
title: WDI_TLV_INTERFACE_CAPABILITIES
description: WDI_TLV_INTERFACE_CAPABILITIES では、Wi-fi インターフェイスの機能を含む TLV です。
ms.assetid: 308331DD-FEEB-4C49-BEBD-117AE58D4792
ms.date: 02/14/2019
keywords:
- WDI_TLV_INTERFACE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 67fb92fede631a8627d019dc8e59268566f43e9a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380755"
---
# <a name="wditlvinterfacecapabilities"></a>WDI\_TLV\_インターフェイス\_機能


WDI\_TLV\_インターフェイス\_機能は、Wi-fi インターフェイスの機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型

0 xf です.

## <a name="length"></a>長さ

含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型 | 説明 |
| --- | --- |
| UINT32 | 最大転送単位 (MTU) のサイズ。 |
| UINT32 | アダプターのマルチキャスト リスト サイズ。 |
| UINT16 | バックフィル サイズ (バイト単位)。 この値は 256 バイトより大きくすることはできません。 |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | アダプターの永続的な MAC アドレス。 デバイスは、複数の永続的な MAC アドレスをサポートする場合は、デバイスによって使用される最初の MAC アドレスが返されます。 |
| UINT32 | サポートされている最大 kbps では、このアダプターの速度を送信します。 |
| UINT32 | サポートされている最大 kbps でこのアダプターのレートを受信します。 |
| UINT8 | ハードウェアによってオプションが有効になっているかどうかを指定します。 有効な値は 0 (無効) および 1 (有効です)。 |
| UINT8 | 指定がオプションかどうかはソフトウェアで有効にします。 有効な値は 0 (無効) および 1 (有効です)。 |
| UINT8 | インターフェイスにサポートしているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 |
| UINT8 | インターフェイスが FLR をサポートしているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 |
| UINT8 | アクションのフレームを送受信することはサポートされているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 |
| UINT8 | RX の空間ストリームのサポートされている数。 |
| UINT8 | テキサス州の空間ストリームのサポートされている数。 |
| UINT8 | アダプター同時に作業できる、操作モードに関係なくチャネルの数。 |
| UINT8 | アンテナの多様性がサポートされているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 |
| UINT8 | ECSA がサポートされているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 |
| UINT8 | アダプターが MAC アドレスのランダム化をサポートするかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 |
 | [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 各アドレス ビットは、ランダム化された (0) または永続的なアドレス (1) と同じ値を保持する必要があります、かどうかを指定するビット マスクです。 既定値はすべて 0 になります。 |
| [**WDI\_BLUETOOTH\_共存\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_bluetooth_coexistence_support) (UINT32) | Wi-fi、Bluetooth の共存のサポートされているレベルです。 |
| UINT8 | WDI 以外の OID のサポートを指定します。 有効な値は次のとおりです。 <ul><li>0 :サポートされません。 Microsoft コンポーネントは、アダプターに転送されていないを理解していない Oid。</li><li>1 :サポートされています。 Microsoft コンポーネントは、アダプターに転送されますを理解していない Oid。</li></ul> <p>これらの Oid には、WDI ヘッダーは含まれません。 要求を受信したアダプターのポートを識別するために使用**NdisPortNumber** NDIS で\_OID\_要求との照合[WDI\_タスク\_を作成します。\_ポート](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)します。</p> |
| UINT8 | 高速の移行がサポートされているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 |
| UINT8 | Mu MIMO がサポートされているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 |
| UINT8 | インターフェイスが Miracast シンクをサポートできないかどうかを指定します。 有効な値は 0 (サポート) および 1 (サポートされていませんです)。 |
| UINT8 | 指定する場合 802.11v BSS 移行がサポートされています。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 |
| UINT8 |  デバイスがドッキング機能 IP をサポートしているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 <p>Windows 10 version 1607 では、バージョン 1.0.21 WDI に追加されます。</p> |
| UINT8 | デバイスが SAE 認証をサポートしているかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 <p>Windows 10、バージョンが 1903 年バージョン 1.1.8 WDI に追加されます。</p> |
| UINT8 | デバイスが Multiband 操作 (MBO) をサポートしているかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 <p>Windows 10、バージョンが 1903 年バージョン 1.1.8 WDI に追加されます。</p> |
| UINT8 | アダプターがビーコン レポートの測定を実装するかどうかを指定します。 有効な値は 0 (アダプターはビーコン レポートの測定を実装していません) および 1 (アダプターは、独自の 11 k ビーコン レポートを実装)。 <p>Windows 10、バージョンが 1903 年バージョン 1.1.8 WDI に追加されます。</p> |

<a name="requirements"></a>必要条件
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

 

 




