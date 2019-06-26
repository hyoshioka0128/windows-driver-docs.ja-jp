---
title: 必須のグラフィックス ドライバー関数
description: 必須のグラフィックス ドライバー関数
ms.assetid: 3a7a7516-b758-4499-bd9d-216fef7b3c8c
keywords:
- GDI WDK Windows 2000 の表示、関数、必要な
- グラフィック ドライバー WDK Windows 2000 を表示するために必要な関数
- 必要な関数、WDK グラフィック
- 必要な描画 WDK GDI、関数、
- GDI WDK Windows 2000 の表示、DDI、必須の関数
- グラフィックス ドライバー WDK Windows 2000 表示、DDI、必要な関数
- DDI WDK グラフィックス、必要な関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d1033ce6b22c478924816db9db2c46b199ec006
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385664"
---
# <a name="required-graphics-driver-functions"></a>必須のグラフィックス ドライバー関数


## <span id="ddk_required_graphics_driver_functions_gg"></span><span id="DDK_REQUIRED_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


すべてのグラフィック ドライバーは GDI 呼び出しを有効にして、ドライバーを無効にするエントリ ポイントをサポートする必要があります、 *PDEV*構造、および各 PDEV に関連付けられている画面。 次の表には、通常は呼び出しがこの順序で必要な関数が一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリ ポイント</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver" data-raw-source="[&lt;strong&gt;DrvEnableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)"><strong>DrvEnableDriver</strong></a></p></td>
<td align="left"><p>初期のドライバーのエントリ ポイントとしてこの関数は、ドライバーのバージョンでサポートされる省略可能な関数の数とエントリ ポイントに GDI を提供します。 これは、GDI を名前で呼び出す唯一のドライバー関数でも。 すべての他のドライバー関数については、関数ポインターのテーブルを通じてアクセスします。 異なり<strong>DrvEnableDriver</strong>、他のドライバーの関数の名前は固定されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetmodes" data-raw-source="[&lt;strong&gt;DrvGetModes&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetmodes)"><strong>DrvGetModes</strong></a></p></td>
<td align="left"><p>指定されたビデオ ハードウェア デバイスでサポートされるモードを一覧表示します。 (この関数は、のディスプレイ ドライバーのみ必要) です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev" data-raw-source="[&lt;strong&gt;DrvEnablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)"><strong>DrvEnablePDEV</strong></a></p></td>
<td align="left"><p>PDEV を有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev" data-raw-source="[&lt;strong&gt;DrvCompletePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)"><strong>DrvCompletePDEV</strong></a></p></td>
<td align="left"><p>デバイスのインストールの完了時にドライバーに通知します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)"><strong>DrvEnableSurface</strong></a></p></td>
<td align="left"><p>指定されたハードウェア デバイスの画面を作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface" data-raw-source="[&lt;strong&gt;DrvDisableSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)"><strong>DrvDisableSurface</strong></a></p></td>
<td align="left"><p>現在のデバイスの作成画面が不要になったドライバーに通知します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev" data-raw-source="[&lt;strong&gt;DrvDisablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)"><strong>DrvDisablePDEV</strong></a></p></td>
<td align="left"><p>ハードウェアを不要になったときは、メモリと、デバイスとは、削除されていない任意の画面で使用されるリソースを解放します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver" data-raw-source="[&lt;strong&gt;DrvDisableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)"><strong>DrvDisableDriver</strong></a></p></td>
<td align="left"><p>ドライバーの割り当てられているすべてのリソースを解放し、デバイスを初期状態に戻します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode" data-raw-source="[&lt;strong&gt;DrvAssertMode&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)"><strong>DrvAssertMode</strong></a></p></td>
<td align="left"><p>指定されたハードウェア デバイスのビデオ モードにリセットします。 (この関数は、のディスプレイ ドライバーのみ必要) です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetdevice" data-raw-source="[&lt;strong&gt;DrvResetDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetdevice)"><strong>DrvResetDevice</strong></a></p></td>
<td align="left"><p>動作不能になったり応答しなくなった場合は、デバイスをリセットします。</p></td>
</tr>
</tbody>
</table>

 

 

 





