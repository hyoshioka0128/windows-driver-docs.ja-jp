---
title: PcAddAdapterDevice ルール (オーディオ)
description: PcAddAdapterDevice ルールは、PortCls ミニポートドライバーが PcAddAdapterDevice 関数を正しく使用することを指定します。具体的には、DeviceExtensionSize はゼロ (0) であるか、またはポートクラスのデバイス拡張サイズ以下である必要があり \_ \_ \_ \_ ます。
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
ms.openlocfilehash: 7fa9b1d656b699e6ff93260c9553401ef57b3973
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917732"
---
# <a name="pcaddadapterdevice-rule-audio"></a>PcAddAdapterDevice ルール (オーディオ)


PcAddAdapterDevice ルールは、PortCls ミニポートドライバーが**pcaddadapterdevice**関数を正しく使用することを指定します。具体的には、 *deviceextensionsize*はゼロ (0) であるか、またはポート \_ クラスのデバイス拡張サイズ以下である必要があり \_ \_ \_ ます。

**ドライバーモデル: オーディオ**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00071007) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>この規則を確認するには、コマンドプロンプトウィンドウを開きます。 Driver Verifier コマンドを入力し、 <strong>/domain audio</strong>を指定します。</p>
<p>たとえば、次のように入力します。</p>
<p><strong>verifier/domain audio</strong> [<em>オプション</em>] <strong>/driver</strong> <em> &lt; ドライバー &gt; </em>の設定</p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





