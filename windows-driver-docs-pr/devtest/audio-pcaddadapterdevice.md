---
title: PcAddAdapterDevice ルール (オーディオ)
description: PcAddAdapterDevice ルール PortCls ミニポート ドライバーが正しく、PcAddAdapterDevice 関数を使用する、DeviceExtensionSize は、ゼロ (0) またはないポート未満のいずれかにすることは、具体的にはよう指定\_クラス\_デバイス\_拡張機能\_サイズ。
ms.assetid: AD020D31-9994-4AD1-A937-E29A594FC9D4
ms.date: 05/21/2018
keywords:
- PcAddAdapterDevice ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcAddAdapterDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de991d7037dd677e0eaa8f0e4a306b62c0f5c4d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527763"
---
# <a name="pcaddadapterdevice-rule-audio"></a>PcAddAdapterDevice ルール (オーディオ)


PcAddAdapterDevice ルールでは、PortCls ミニポート ドライバーが正しく使用を指定します、 **PcAddAdapterDevice**を具体的には、関数、 *DeviceExtensionSize*ゼロ (0) または no のいずれかにする必要があります小さいポート\_クラス\_デバイス\_拡張子\_サイズ。

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00071007) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>このルールを確認するには、コマンド プロンプト ウィンドウを開きます。 Driver Verifier のコマンドを入力し、指定<strong>/domain オーディオ</strong>します。</p>
<p>次に、例を示します。</p>
<p><strong>verifier /domain audio</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





