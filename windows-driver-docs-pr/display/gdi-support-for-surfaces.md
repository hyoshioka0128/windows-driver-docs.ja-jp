---
title: サーフェスの GDI サポート
description: サーフェスの GDI サポート
ms.assetid: 78c1e09d-8c3e-4c5d-b670-2e4adf77814f
keywords:
- DrvEnableSurface
- DrvDisableSurface
- GDI WDK Windows 2000 の表示、サーフェス
- グラフィックス ドライバー WDK Windows 2000 の表示、サーフェス
- WDK の GDI やサーフェスの描画
- 画面を有効にして、GDI の WDK を無効化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77d109010c3a36cfa42eef6b63a16e336ba4179a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384560"
---
# <a name="gdi-support-for-surfaces"></a>サーフェスの GDI サポート


## <span id="ddk_gdi_support_for_surfaces_gg"></span><span id="DDK_GDI_SUPPORT_FOR_SURFACES_GG"></span>


各*PDEV*、ドライバーをサポートする必要があります、 [ **DrvEnableSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff556214)関数。 *DrvEnableSurface*描画する表面を設定し、PDEV に関連付けます。 ドライバーをサポートする必要がありますも、 [ **DrvDisableSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff556200)サーフェスの作成を無効にする関数。 GDI を作成し、画面の維持、ため、ドライバーは、有効にして、サーフェスの無効化を実装するために、次の表に、いくつかの GDI サービス関数に依存します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数名</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564183" data-raw-source="[&lt;strong&gt;EngAssociateSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564183)"><strong>EngAssociateSurface</strong></a></p></td>
<td align="left"><p>サーフェスを関連付けます、PDEV し、ドライバーの作成者が表示されるをフックする必要が描画操作を定義します。 PDEV の既定のパレットとスタイルの手順を使用します。 ドライバーの実行中にプライマリ サーフェイスでのこの呼び出しを行う必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff556214" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556214)"> <strong>DrvEnableSurface</strong></a>します。 ドライバーでは、有効にすると、セカンダリのサーフェイスを記述する画面をロックする前にこの呼び出しを加える必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564189" data-raw-source="[&lt;strong&gt;EngCheckAbort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564189)"><strong>EngCheckAbort</strong></a></p></td>
<td align="left"><p>(プリンターのみ)印刷ジョブが終了したかどうかを判断するプリンタ ドライバを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564199" data-raw-source="[&lt;strong&gt;EngCreateBitmap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564199)"><strong>EngCreateBitmap</strong></a></p></td>
<td align="left"><p>標準の形式を作成します。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-independent-bitmap--dib-" data-raw-source="&lt;em&gt;DIB&lt;/em&gt;"> <em>DIB</em> </a>ビットマップ。 GDI は、この種類の画面上のすべての描画操作を実行できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564204" data-raw-source="[&lt;strong&gt;EngCreateDeviceBitmap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564204)"><strong>EngCreateDeviceBitmap</strong></a></p></td>
<td align="left"><p>(ただし、これをケース ドライバー コールバックする GDI 描画して、DIB として作成できます) に描画する場合、ドライバーはデバイス依存ビットマップを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564206" data-raw-source="[&lt;strong&gt;EngCreateDeviceSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564206)"><strong>EngCreateDeviceSurface</strong></a></p></td>
<td align="left"><p>作成、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surface&lt;/em&gt;"><em>画面のデバイスで管理された</em></a>します。 ドライバーはこのサーフェスの特定の描画操作の管理を担当します。 関数は、ドライバーを管理するハンドルを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564769" data-raw-source="[&lt;strong&gt;EngCreateWnd&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564769)"><strong>EngCreateWnd</strong></a></p></td>
<td align="left"><p>作成、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff570599" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570599)"> <strong>WNDOBJ</strong> </a>指定した表面に構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564827" data-raw-source="[&lt;strong&gt;EngDeleteSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564827)"><strong>EngDeleteSurface</strong></a></p></td>
<td align="left"><p>サーフェス (DIB、デバイス依存ビットマップ、または画面のデバイス管理) を削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564830" data-raw-source="[&lt;strong&gt;EngDeleteWnd&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564830)"><strong>EngDeleteWnd</strong></a></p></td>
<td align="left"><p>削除、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff570599" data-raw-source="[&lt;strong&gt;WNDOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570599)"> <strong>WNDOBJ</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564857" data-raw-source="[&lt;strong&gt;EngEraseSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564857)"><strong>EngEraseSurface</strong></a></p></td>
<td align="left"><p>指定した色になっているため、それを効果的に消去では、サーフェイス上の指定した四角形を塗りつぶします。 GDI ビットマップの表面を消去するのみ、この関数を呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564966" data-raw-source="[&lt;strong&gt;EngLockDirectDrawSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564966)"><strong>EngLockDirectDrawSurface</strong></a></p></td>
<td align="left"><p>DirectDraw surface のカーネル モードのハンドルをロックします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564968" data-raw-source="[&lt;strong&gt;EngLockSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564968)"><strong>EngLockSurface</strong></a></p></td>
<td align="left"><p>ユーザー オブジェクトを作成して、作成した画面にドライバー アクセス権を与えます (<a href="https://msdn.microsoft.com/library/windows/hardware/ff569901" data-raw-source="[&lt;strong&gt;SURFOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569901)"><strong>SURFOBJ</strong></a>) 表示されるのです。 (、<a href="surface-negotiation.md" data-raw-source="[primary surface](surface-negotiation.md)">プライマリ サーフェス</a>はロックされていません)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564975" data-raw-source="[&lt;strong&gt;EngMarkBandingSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564975)"><strong>EngMarkBandingSurface</strong></a></p></td>
<td align="left"><p>(プリンターのみ)バンドの画面としてサーフェスをマークします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564976" data-raw-source="[&lt;strong&gt;EngModifySurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564976)"><strong>EngModifySurface</strong></a></p></td>
<td align="left"><p>ドライバーによって作成された画面の属性については、GDI を通知します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565042" data-raw-source="[&lt;strong&gt;EngUnlockDirectDrawSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565042)"><strong>EngUnlockDirectDrawSurface</strong></a></p></td>
<td align="left"><p>特定の DirectDraw 指定した画面のロックを解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565422" data-raw-source="[&lt;strong&gt;EngUnlockSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565422)"><strong>EngUnlockSurface</strong></a></p></td>
<td align="left"><p>ドライバーの描画操作が完了すると、画面のロックを解除 (無効にするときに呼び出される、<a href="surface-negotiation.md" data-raw-source="[secondary surface](surface-negotiation.md)">セカンダリ画面</a>)。</p></td>
</tr>
</tbody>
</table>

 

 

 





