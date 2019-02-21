---
title: 必要なディスプレイ ドライバー関数
description: 必要なディスプレイ ドライバー関数
ms.assetid: 483aa13b-a14d-49f3-8265-013f7bb64d40
keywords:
- グラフィックス DDI 関数 WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1e78c22763f499f34720b102834224ff6539976
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532128"
---
# <a name="required-display-driver-functions"></a>必要なディスプレイ ドライバー関数


## <span id="ddk_required_display_driver_functions_gg"></span><span id="DDK_REQUIRED_DISPLAY_DRIVER_FUNCTIONS_GG"></span>


少なくとも、すべてのディスプレイ ドライバーが必要です。

1.  有効にして、グラフィックス ハードウェアを無効にします。

2.  GDI は、ハードウェアの機能に関する情報を指定します。

3.  描画サーフェイスを有効にします。

次の表のドライバーをすべて表示する関数を実装する必要があります。 次の**DrvEnableDriver**、残りの関数がアルファベット順に一覧表示されます。 除く**DrvEnableDriver**どの GDI を名前で呼び出す、他のすべてのディスプレイ ドライバー関数が固定の名前がないと pseudonames と共に一覧表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556210" data-raw-source="[&lt;strong&gt;DrvEnableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556210)"><strong>DrvEnableDriver</strong></a></p></td>
<td align="left"><p>ドライバーの初期のエントリ ポイントとして提供 GDI ドライバーのバージョンでサポートされる省略可能な関数の数とエントリ ポイント。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556178" data-raw-source="[&lt;strong&gt;DrvAssertMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556178)"><strong>DrvAssertMode</strong></a></p></td>
<td align="left"><p>指定されたビデオ ハードウェア デバイスのビデオ モードにリセットします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556181" data-raw-source="[&lt;strong&gt;DrvCompletePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556181)"><strong>DrvCompletePDEV</strong></a></p></td>
<td align="left"><p>デバイスのインストールの完了に関するドライバーに通知します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556196" data-raw-source="[&lt;strong&gt;DrvDisableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556196)"><strong>DrvDisableDriver</strong></a></p></td>
<td align="left"><p>ドライバーの割り当てられているすべてのリソースを解放し、デバイスを最初に読み込まれた状態に戻します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556198" data-raw-source="[&lt;strong&gt;DrvDisablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556198)"><strong>DrvDisablePDEV</strong></a></p></td>
<td align="left"><p>ハードウェアを不要になったときは、メモリと、デバイスとは、削除されていない任意の画面で使用されるリソースを解放します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556200" data-raw-source="[&lt;strong&gt;DrvDisableSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556200)"><strong>DrvDisableSurface</strong></a></p></td>
<td align="left"><p>現在のデバイスの作成画面が不要になったドライバーに通知します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556211" data-raw-source="[&lt;strong&gt;DrvEnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556211)"><strong>DrvEnablePDEV</strong></a></p></td>
<td align="left"><p>により、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556325#wdkgloss-pdev" data-raw-source="&lt;em&gt;PDEV&lt;/em&gt;"> <em>PDEV</em></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556214" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556214)"><strong>DrvEnableSurface</strong></a></p></td>
<td align="left"><p>指定されたハードウェア デバイスの画面を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556233" data-raw-source="[&lt;strong&gt;DrvGetModes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556233)"><strong>DrvGetModes</strong></a></p></td>
<td align="left"><p>指定されたビデオ ハードウェア デバイスでサポートされるモードを一覧表示します。</p></td>
</tr>
</tbody>
</table>

 

すべてのグラフィック ドライバーを必要な関数の一覧に表示されます[必要なグラフィックス ドライバー関数](required-graphics-driver-functions.md)します。

 

 





