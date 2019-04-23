---
title: OID_WDI_SET_ADAPTER_CONFIGURATION
description: OID_WDI_SET_ADAPTER_CONFIGURATION は、アダプターを構成します。 オプションのプロパティし、任意のポートを作成する前にのみ送信できます。
ms.assetid: d1c37943-4755-4b9e-ab9c-9378aeca9c03
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ADAPTER_CONFIGURATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e7fe2a1cb746e720cffdafbd51c09c5f766ec5d9
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902348"
---
# <a name="oidwdisetadapterconfiguration"></a>OID\_WDI\_設定\_アダプター\_構成


OID\_WDI\_設定\_アダプター\_構成がアダプターを構成します。 オプションのプロパティし、任意のポートを作成する前にのみ送信できます。

| Scope   | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|---------|--------------------------|---------------------------------|
| [アダプター] | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>許可されている複数の TLV インスタンス</th>
<th>省略可能</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926257" data-raw-source="[&lt;strong&gt;WDI_TLV_CONFIGURED_MAC_ADDRESS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926257)"><strong>WDI_TLV_CONFIGURED_MAC_ADDRESS</strong></a></td>
<td></td>
<td>x</td>
<td>MAC アドレスです。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898075" data-raw-source="[&lt;strong&gt;WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898075)"><strong>WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD</strong></a></td>
<td></td>
<td>x</td>
<td>到達不能検出のしきい値。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897879" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897879)"><strong>WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY</strong></a></td>
<td></td>
<td>x</td>
<td>停止/再起動、Wi-Fi Direct 移動をリセットした後、チャネルの選択を操作するために、ファームウェアによって使用されるポリシー。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926145" data-raw-source="[&lt;strong&gt;WDI_TLV_BAND_ID_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926145)"><strong>WDI_TLV_BAND_ID_LIST</strong></a></td>
<td></td>
<td>x</td>
<td>バンド Id の一覧です。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897841" data-raw-source="[&lt;strong&gt;WDI_TLV_LINK_QUALITY_BAR_MAP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897841)"><strong>WDI_TLV_LINK_QUALITY_BAR_MAP</strong></a></td>
<td></td>
<td></td>
<td>信号の品質、Wi-fi 信号の強さバーへのマッピングです。 アダプターによってこのフィールドを無視するかで指定された動作を使用する必要があります<a href="ndis-status-wdi-indication-link-state-change.md" data-raw-source="[NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE](ndis-status-wdi-indication-link-state-change.md)">NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE</a>リンクの品質の通知を行うためです。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/mt269108" data-raw-source="[&lt;strong&gt;WDI_TLV_ADAPTER_NLO_SCAN_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt269108)"><strong>WDI_TLV_ADAPTER_NLO_SCAN_MODE</strong></a></td>
<td></td>
<td>x</td>
<td>アクティブまたはパッシブ モードで NLO スキャンを実行するかどうかを示します。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/mt593243" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593243)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a></td>
<td></td>
<td></td>
<td>Windows 10 バージョン 1511、WDI バージョン 1.0.10 に追加されます。
<p>PLDR がサポートされているかどうかを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。

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

 

 




