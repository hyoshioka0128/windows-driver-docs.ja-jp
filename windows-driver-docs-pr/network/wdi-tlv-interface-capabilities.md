---
title: WDI_TLV_INTERFACE_CAPABILITIES
description: WDI_TLV_INTERFACE_CAPABILITIES は、Wi-fi インターフェイスの機能を含む TLV です。
ms.assetid: 308331DD-FEEB-4C49-BEBD-117AE58D4792
ms.date: 02/14/2019
keywords:
- WDI_TLV_INTERFACE_CAPABILITIES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 8a8ac3197fabc54e1e15c8ad68fed8552111184c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842468"
---
# <a name="wdi_tlv_interface_capabilities"></a>WDI\_TLV\_インターフェイス\_の機能


WDI\_TLV\_インターフェイス\_機能は、Wi-fi インターフェイスの機能を含む TLV です。

## <a name="tlv-type"></a>TLV 型

0Xf です

## <a name="length"></a>長さ

含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに | 説明 |
| --- | --- |
| UINT32 | 最大転送単位 (MTU) のサイズ。 |
| UINT32 | アダプターのマルチキャストリストのサイズ。 |
| UINT16 | バイト単位のバックフィルサイズ。 この値を256バイトより大きくすることはできません。 |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | アダプターの永続的な MAC アドレス。 デバイスが複数の永続的な MAC アドレスをサポートしている場合は、デバイスによって使用される最初の MAC アドレスが返されます。 |
| UINT32 | このアダプターでサポートされる最大送信速度 (kbps)。 |
| UINT32 | このアダプターでサポートされる最大受信速度 (kbps)。 |
| UINT8 | 無線がハードウェアによって有効かどうかを指定します。 有効な値は 0 (無効) と 1 (有効) です。 |
| UINT8 | ソフトウェアによってラジオが有効かどうかを指定します。 有効な値は 0 (無効) と 1 (有効) です。 |
| UINT8 | インターフェイスが PLR をサポートするかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 |
| UINT8 | インターフェイスが FLR をサポートするかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 |
| UINT8 | アクションフレームの送信と受信がサポートされているかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 |
| UINT8 | サポートされている RX 空間ストリームの数。 |
| UINT8 | サポートされている TX 空間ストリームの数。 |
| UINT8 | 操作モードに関係なく、アダプターが同時に使用できるチャネルの数。 |
| UINT8 | アンテナの多様性をサポートするかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 |
| UINT8 | ECSA がサポートされているかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 |
| UINT8 | アダプターが MAC アドレスのランダム化をサポートするかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 |
 | [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ランダム (0) にするか、永続的なアドレス (1) と同じ値を保持するかどうかを、各アドレスビットに対して指定するビットマスク。 既定値はすべて0です。 |
| [**WDI\_BLUETOOTH\_の共存\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bluetooth_coexistence_support)(UINT32) | Wi-fi Bluetooth のサポートされているレベル。 |
| UINT8 | 非 WDI OID サポートを指定します。 有効な値は次のとおりです。 <ul><li>0: サポートされていません。 Microsoft コンポーネントで認識されない Oid はアダプターに転送されません。</li><li>1: サポートされています。 Microsoft コンポーネントで認識されない Oid はアダプターに転送されます。</li></ul> <p>これらの Oid には、WDI ヘッダーは含まれません。 要求が発生したアダプターのポートを特定するには、NDIS\_OID\_要求で**Ndisportnumber**を使用し、 [WDI\_タスク\_\_ポートを作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)します。</p> |
| UINT8 | 高速な移行がサポートされているかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 |
| UINT8 | MIMO がサポートされているかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 |
| UINT8 | インターフェイスが Miracast シンクをサポートできないかどうかを指定します。 有効な値は 0 (サポートされています) と 1 (サポートされていません) です。 |
| UINT8 | 802.11 v BSS の移行がサポートされているかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 |
| UINT8 |  デバイスが IP ドッキング機能をサポートするかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 <p>Windows 10 バージョン1607、WDI version 1.0.21 に追加されました。</p> |
| UINT8 | デバイスが SAE 認証をサポートするかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 <p>Windows 10 バージョン1903、WDI version 1.1.8 に追加されました。</p> |
| UINT8 | デバイスがマルチバンド操作 (MBO) をサポートするかどうかを指定します。 有効な値は、0 (サポートされていません) と 1 (サポートされています) です。 <p>Windows 10 バージョン1903、WDI version 1.1.8 に追加されました。</p> |
| UINT8 | アダプターがビーコンレポートの測定値を実装するかどうかを指定します。 有効な値は 0 (アダプターはビーコンレポートの測定値を実装しません) と 1 (アダプターは独自の 11 k ビーコンレポートを実装します) です。 <p>Windows 10 バージョン1903、WDI version 1.1.8 に追加されました。</p> |

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




