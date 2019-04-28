---
title: 元のインターフェイス
description: 元のインターフェイス
ms.assetid: 78f1e722-c2bd-4232-96f1-71df7e6ece23
keywords:
- ジョイスティックに WDK を非表示にインターフェイス
- 仮想ジョイスティックのドライバー WDK を非表示にインターフェイス
- VJoyD WDK HID、インターフェイス
- WDK ジョイスティック インターフェイス
- ジョイスティックに WDK を非表示にコールバック
- 仮想ジョイスティックのドライバー WDK を非表示にコールバック
- VJoyD WDK HID、コールバック
- WDK ジョイスティックのコールバック
- WDK ジョイスティックのポーリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f3207028979b5fd028a9303155e988e764255d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372966"
---
#  <a name="original-interface"></a>元のインターフェイス





次のジョイスティック ミニドライバー コールバックは、元のインターフェイスに固有します。

-   A[ポーリング コールバック](polling-callback.md)ジョイスティックの位置とボタンの情報を返します。

-   A [Configuration Manager のコールバック](configuration-manager-callback.md)Windows 95 で configuration manager のメッセージを処理します。

-   A[ハードウェア機能コールバック](hardware-capabilities-callback.md)ジョイスティック機能に対する要求を処理します。

-   A[ジョイスティック識別コールバック](joystick-identification-callback.md)VJoyD、ジョイスティックのミニドライバーを通知するために使用するへの応答が。

VJoyD VJOYD に 4 つのジョイスティックに固有のコールバックを登録する必要があります\_登録\_デバイス\_SYS を処理から戻る前に、ドライバー サービス\_動的\_デバイス\_INIT メッセージ。 EAX は、ポーリングのルーチン、EBX (構成ハンドラー)、(機能コールバック) の場合は、ECX および EDX (識別ルーチン) を指す必要があります。 ジョイスティック ミニドライバーの登録のシーケンスの例は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>mov</p></td>
<td><p>eax、offset32 _PollRoutine@8</p></td>
</tr>
<tr class="even">
<td><p>mov</p></td>
<td><p>ebx、offset32 _CfgRoutine</p></td>
</tr>
<tr class="odd">
<td><p>mov</p></td>
<td><p>ecx に offset32 _HWCapsRoutine@8</p></td>
</tr>
<tr class="even">
<td><p>mov</p></td>
<td><p>edx、offset32 _JoyIdRoutine@8</p></td>
</tr>
<tr class="odd">
<td><p>VxDcall</p></td>
<td><p>VJOYD_Register_Device_Driver</p></td>
</tr>
</tbody>
</table>

 

ミニドライバーは、登録に加えて、この時点で他の初期化を実行することができます。 ジョイスティック ミニドライバーのモデルには、SYS への応答で特定のアクションは不要\_動的\_デバイス\_VxD 引き続き使用することが最終的なクリーンアップを内部の場合、終了します。

 

 




