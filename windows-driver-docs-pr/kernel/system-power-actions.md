---
title: システム電源操作
description: システム電源操作
ms.assetid: e8ab99d4-c18d-4ba8-bfe8-8eebb881c384
keywords:
- システム電源操作 WDK 電源管理
- システム電源の状態の WDK カーネル、電源操作
- 電源操作 WDK 電源管理
- POWER_ACTION
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cea2bcdfd67fe50f4a505e3cb23622b72d6a5eec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530673"
---
# <a name="system-power-actions"></a>システム電源操作





電源マネージャーは、設定またはシステムの電源状態をクエリする IRP を送信するときは、電源状態の変更に関する情報を提供する追加のパラメーターと共にシステム電源の状態を指定します。 このパラメーターが渡される**Irp -&gt;Parameters.Power.ShutdownType**、電源の列挙子は、\_アクションの種類。 列挙子では、次の表に示すように、システム電源の状態要求が特徴です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>POWER_ACTION 列挙子</th>
<th>要求されたシステム電源の状態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PowerActionNone</strong></p></td>
<td><p>S0 またはないシステム電源の IRP アクティブ</p></td>
</tr>
<tr class="even">
<td><p><strong>PowerActionSleep</strong></p></td>
<td><p>S1、S2 または S3</p></td>
</tr>
<tr class="odd">
<td><p><strong>PowerActionHibernate</strong></p></td>
<td><p>S4</p></td>
</tr>
<tr class="even">
<td><p><strong>PowerActionShutdown</strong> (Microsoft Windows 2000 およびそれ以降のシステムのみ)</p></td>
<td><p>S5</p></td>
</tr>
<tr class="odd">
<td><p><strong>PowerActionShutdownReset</strong></p></td>
<td><p>S5</p></td>
</tr>
<tr class="even">
<td><p><strong>PowerActionShutdownOff</strong></p></td>
<td><p>S5</p></td>
</tr>
</tbody>
</table>

 

ドライバー S5 のシステム クエリまたはセット power IRP を受け取ると、確認できる**ShutdownType**詳細については、要求されたシャット ダウンします。 ドライバーは、電源を無期限にシャット ダウンではなく、マシンをリセットする際に、シャット ダウン シーケンスを最適化するために、この情報を使用できます。 ほとんどのデバイスのドライバーは、システムがリセットされたときに電源を保持します。 ただし、ダイレクト メモリ アクセス (DMA) を実行するデバイスをストリーミング ビデオなど、特定のデバイス ドライバーこともできます、デバイスの電源をシステムをリセットすると、そのため、継続的な I/O を停止するときに。

デバイスの電源ポリシー所有者に送信すると、*デバイス*IRP の電源システム電源 IRP への応答でそのデバイス スタックにドライバーを使用できる、 **ShutdownType**現在に関する情報を取得するパラメーター*システム*IRP の電源をします。 この例では、値で**ShutdownType**現在要求されているシステムの電源状態を示しますがまたは**PowerActionNone**システム要求が存在しない場合。 ドライバーは、ただし、依存しないこの情報デバイス IRP の要求状態 D0 場合。

Windows 98 ではこのメンバーが常に格納する、/ **PowerActionNone** IRP がデバイスの電源状態を要求したときにします。

 

 




