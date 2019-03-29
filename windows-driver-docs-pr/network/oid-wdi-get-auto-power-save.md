---
title: OID_WDI_GET_AUTO_POWER_SAVE
description: OID_WDI_GET_AUTO_POWER_SAVE、省電力、ポートの状態を取得します。
ms.assetid: b7a14348-66ad-4728-986d-05145eb49b27
ms.date: 07/18/2017
keywords:
- OID_WDI_GET_AUTO_POWER_SAVE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dc34e729070cc62dccb6fc3069b4767f8fc56c13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579503"
---
# <a name="oidwdigetautopowersave"></a>OID\_WDI\_取得\_自動\_POWER\_保存


OID\_WDI\_取得\_自動\_POWER\_保存、省電力、ポートの状態を取得します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 適用なし           | 1                               |

 

省電力と待機時間の間にトレードオフがあります。 有効にする自動省電力モードを設定すると、 [OID\_WDI\_設定\_接続\_品質](oid-wdi-set-connection-quality.md)コマンド、ファームウェアに進むには接続されているアクセス ポイントと対話しようとしました。省電力モードとして、電力を節約する適切です。 ファームウェアも、接続されているアクセス ポイントが、802.11 仕様に、省電力モード プロトコルに依存して場合を検出できます。 アクセス ポイントが準拠していない場合 (は省電力モードを正しくサポートしない)、自動電源の保存が無効に設定している場合でもファームウェアが省電力モードに移動しない必要があります。 自動電源の保存を無効に設定、ファームウェアのパケットを送受信する際の低待機時間について説明します。 これは、ストリーミングのモードがオンのとき、および低待機時間が節電優先されるため、システムは AC 電源を使用してあります。

## <a name="get-property-parameters"></a>プロパティのパラメーターを取得します。


追加のパラメーターはありません。 ヘッダー内のデータで十分です。
## <a name="get-property-results"></a>プロパティの結果を得る


| TLV                                                                          | 許可されている複数の TLV インスタンス | 省略可能 | 説明                  |
|------------------------------------------------------------------------------|--------------------------------|----------|------------------------------|
| [**WDI\_TLV\_取得\_自動\_POWER\_保存**](https://msdn.microsoft.com/library/windows/hardware/dn926307) |                                |          | 自動電源は、情報を保存します。 |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




