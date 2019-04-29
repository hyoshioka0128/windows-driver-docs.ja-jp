---
Description: WinUSB 電源管理
title: WinUSB 電源管理
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: d4c57bfa041744eba9129e67c1097f4da5a0be0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389143"
---
# <a name="winusb-power-management"></a>WinUSB 電源管理


WinUSB は、電源管理の KMDF のステート マシンを使用します。 呼び出しを通じて電源ポリシーの管理は[ **WinUsb\_SetPowerPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff540309)します。

WinUSB の電源の動作を変更するには、デバイスの INF で既定のレジストリ設定を変更できます。 内の値を追加することで、レジストリにデバイスの特定の場所にこれらの値を記述する必要があります、 **HW。AddReg** INF のセクション。

電源動作を変更するデバイスの INF では、次の一覧で説明するレジストリ値を指定できます。

<a href="" id="system-wake"></a>**システム スリープ解除**  
この機能は制御、 **SystemWakeEnabled** DWORD のレジストリ設定します。 この値は、デバイスが省電力状態からシステムをスリープ解除できるかどうかを示します。

```INF
HKR,,SystemWakeEnabled,0x00010001,1
```

-   値 0、またはこの値がない場合は、システムをスリープ解除するデバイスが許可されないことを示します。
-   システムをスリープ解除するデバイスを許可するのには、設定**SystemWakeEnabled** 0 以外の値。 デバイスのチェック ボックスを**プロパティ**ユーザー設定を上書きできるように、ページが自動的に有効にします。

**注**  Changing、 **SystemWakeEnabled**設定には、中断選択的には影響はありません、このレジストリ値がシステムにのみ関係を中断します。

 

<a href="" id="selective-suspend"></a>**選択的な中断**  
セレクティブ サスペンドのいくつかのシステムまたは WinUSB 設定によって無効にすることができます。 1 つの設定を強制はできません WinUSB 有効にする選択的中断します。

次のポリシー設定で指定されている電源[ **WinUsb\_SetPowerPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff540309)の*PolicyType*パラメーターの選択的な動作に影響します。中断します。

-   自動\_中断時に、0 に設定は設定しません、デバイス セレクティブ サスペンド モード。
-   中断\_遅延セット WinUSB が選択的に移動するデバイスを要求したときに、デバイスがアイドル状態までの時間を中断します。

次の表では、レジストリ キーがセレクティブ サスペンド機能に与える影響を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>レジストリ キー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>DeviceIdleEnabled</strong></td>
<td>これは、DWORD 値です。 このレジストリ値では、(セレクティブ サスペンド) アイドル時、デバイスが電源できるかどうかを示します。
<ul>
<li>値 0、またはこの値がない場合は、デバイス サポートしていないことの電源を示します。 アイドル状態のときにダウンします。</li>
<li>0 以外の値は、アイドル状態のときに電源、デバイスがサポートを示します。</li>
<li>DeviceIdleEnabled が設定されていない場合、AUTO_SUSPEND 電源ポリシーの設定の値は無視されます。</li>
</ul>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,DeviceIdleEnabled,0x00010001,1</code></pre></td>
</tr>
<tr class="even">
<td><strong>DeviceIdleIgnoreWakeEnable</strong></td>
<td>RemoteWake サポートしていない場合でも、デバイスを中断、0 以外の値に設定すると、します。</td>
</tr>
<tr class="odd">
<td><strong>UserSetDeviceIdleEnabled</strong></td>
<td>この値は、DWORD 値です。 このレジストリ値では、チェック ボックスをデバイスで有効にするかどうかを示します<strong>プロパティ</strong>アイドル状態の既定値を上書きするユーザーを許可するページ。 ときに<strong>UserSetDeviceIdleEnabled</strong>設定が 0 以外の値のチェック ボックスが有効になっているし、ユーザーがアイドル状態のときに、デバイスの電源を無効にできます。 値 0、またはこの値がない場合は、チェック ボックスが有効でないことを示します。
<ul>
<li>ユーザーがデバイスの電力の削減を無効にする場合、AUTO_SUSPEND 電源ポリシーの設定の値は無視されます。</li>
<li>ユーザーがデバイスの電力の削減を有効の場合、アイドル状態のときに、デバイスを中断するかどうかを判断する AUTO_SUSPEND の値が使用されます。</li>
</ul>
<p><strong>UserSetDeviceIdleEnabled</strong>場合は無視されます<strong>DeviceIdleEnabled</strong>が設定されていません。</p>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,UserSetDeviceIdleEnabled,0x00010001,1</code></pre></td>
</tr>
<tr class="even">
<td><strong>DefaultIdleState</strong></td>
<td>これは、DWORD 値です。 このレジストリ値は、AUTO_SUSPEND 電源ポリシーの設定の既定値を設定します。 このレジストリ キーが有効または無効、選択的に使用されるハンドルがデバイスに開いていないときに中断します。
<ul>
<li>この値がない場合または 0 の値を既定では、デバイスが中断されていないときにアイドル状態を示します。 デバイスをアイドル状態のときに中断すると、AUTO_SUSPEND 電源ポリシーが有効になっている場合にのみ許可。</li>
<li>0 以外の値は、既定では、デバイスが許可されているアイドル状態のときに中断されることを示します。</li>
</ul>
<p>場合、この値は無視されます<strong>DeviceIdleEnabled</strong>が設定されていません。</p>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,DefaultIdleState,0x00010001,1</code></pre></td>
</tr>
<tr class="odd">
<td><strong>DefaultIdleTimeout</strong></td>
<td>これは、DWORD 値です。 このレジストリ値は、SUSPEND_DELAY 電源ポリシーの設定の既定の状態を設定します。
<p>値は、デバイスがアイドル状態であると判断する前に待機するミリ秒単位の時間を示します。</p>
<pre class="syntax" space="preserve"><code class="language-INF">HKR,,DefaultIdleTimeout,0x00010001,100</code></pre></td>
</tr>
</tbody>
</table>

 

<a href="" id="detecting-idle"></a>**アイドル状態の検出**  
強制的にデバイスのすべての書き込みと制御の転送、 **D0**電源の状態と、アイドル タイマーをリセットします。 エンドポイント キューは、電源管理の対象ではありません。 読み取り要求は、自分が送信したときに、デバイスをスリープ解除します。 ただし、デバイスに読み取り要求を待機中にアイドル状態。

## <a name="related-topics"></a>関連トピック
[WinUSB アーキテクチャとモジュール](winusb-architecture.md)  
[USB クライアント ドライバーを開発するためのドライバー モデルの選択](winusb-considerations.md)  
[WinUSB (Winusb.sys) のインストール](winusb-installation.md)  
[WinUSB 関数を使用して、USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)  
[ポリシーの変更をパイプ WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 関数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)  
[WinUSB](winusb.md)  
[**WinUsb\_GetPowerPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff540275)  
[**WinUsb\_SetPowerPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff540309)  



