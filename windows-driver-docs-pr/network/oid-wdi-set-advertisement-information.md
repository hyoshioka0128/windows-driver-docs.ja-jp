---
title: OID_WDI_SET_ADVERTISEMENT_INFORMATION
description: OID_WDI_SET_ADVERTISEMENT_INFORMATION は、probe 要求、プローブ応答、および指定されたポートによって送信されるビーコンに含まれる情報要素 (IEs) とその他の提供情報の設定を構成します。
ms.assetid: efa1fc93-2cc8-4d14-be5f-d099ef3c371e
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ADVERTISEMENT_INFORMATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 234a9a733e924990ad39668c2ad04f434929d683
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560201"
---
# <a name="oidwdisetadvertisementinformation"></a>OID\_WDI\_設定\_広告\_情報


OID\_WDI\_設定\_広告\_情報プローブ要求、プローブ応答、およびによって送信されるビーコンに含まれる情報要素 (IEs) とその他の提供情報の設定を構成します、指定されたポート。 この要求では、Wi-Fi Direct ポートに適用のみです。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

デバイスで、このコマンドが受信したときに、すべての関連する Wi-Fi Direct IEs を更新し、将来的に送信するメッセージがこのポートから送信されたすべての必要な追加 IEs を追加、ものとします。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


WDI は、提供するサービスの構成済みの一連のプレフィックス ハッシュを指定できます。 ピアは、ハッシュを送信する場合、ドライバーがで定義されているサービス名のハッシュと一致するようにまず[ **WDI\_TLV\_P2P\_アドバタイズ\_プレフィックス\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/mt269134). サービス、ドライバーを検索プレフィックス ハッシュの一致が見つかった場合[ **WDI\_TLV\_P2P\_アドバタイズ\_サービス\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/dn897861)プレフィックスがあり、これらは応答をします。 ドライバーが要求されたサービス名のハッシュと一致しようとした、一致が見つからない場合[ **WDI\_TLV\_P2P\_アドバタイズ\_サービス\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/dn897861).

| TLV                                                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                     |
|-----------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI\_TLV\_追加\_IES**](https://msdn.microsoft.com/library/windows/hardware/dn926122)                                    |                                | X        | 含まれる IEs を追加します。                  |
| [**WDI\_TLV\_P2P\_デバイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn897875)                                 |                                | X        | Wi-Fi Direct デバイス情報。                |
| [**WDI\_TLV\_P2P\_デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/dn897872)                     |                                | X        | Wi-Fi Direct デバイス機能。               |
| [**WDI\_TLV\_P2P\_グループ\_所有者\_機能**](https://msdn.microsoft.com/library/windows/hardware/dn897954)          |                                | X        | グループ所有者を Wi-Fi Direct 機能情報 |
| [**WDI\_TLV\_P2P\_SECONDARY\_DEVICE\_TYPE\_LIST**](https://msdn.microsoft.com/library/windows/hardware/dn897991) |                                | X        | Wi-Fi Direct のセカンダリ デバイスの種類の一覧です。    |
| [**WDI\_TLV\_P2P\_アドバタイズ\_サービス**](https://msdn.microsoft.com/library/windows/hardware/dn897860)                 |                                | X        | Wi-Fi Direct サービスを提供します。               |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。
## <a name="unsolicited-indication"></a>要請されていないを示す値


[NDIS\_状態\_WDI\_INDICATION\_アクション\_フレーム\_RECEIVED](ndis-status-wdi-indication-action-frame-received.md)アダプターは、場合に、サービスについての ANQP 操作フレームの要求を示す必要があります、ピアから ANQP 要求を (またはその他の不明なアクションのフレーム) を受信します。

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




