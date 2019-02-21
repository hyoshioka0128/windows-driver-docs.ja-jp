---
title: SPB コント ローラーのドライバー
description: SPB のコント ローラーは、シンプルな周辺機器バス (SPB) を制御し、SPB に接続されている周辺機器とデータを転送するデバイスです。
ms.assetid: 046353F9-315F-4328-8ECA-1C23AF87B4B4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfb56a5d4d05e8a7fa5c6200166555509523e6ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556514"
---
# <a name="spb-controller-drivers"></a>SPB コント ローラーのドライバー


SPB のコント ローラーが制御するデバイスを[シンプルな周辺機器のバス](https://msdn.microsoft.com/library/windows/hardware/hh450903)(SPB) SPB に接続されている周辺機器とデータを転送するとします。 SPB コント ローラーのハードウェア ベンダーは、コント ローラーのハードウェア機能を管理する SPB コント ローラーのドライバーを提供します。

簡略化のコント ローラーのドライバーの開発を SPB フレームワーク拡張機能 (SpbCx) Windows 8 以降、[単純な周辺機器のバス](https://msdn.microsoft.com/library/windows/hardware/hh450903)(SPBs)。 SpbCx がするシステム提供の拡張機能、[カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF)。 SPB コント ローラー デバイスのハードウェア ベンダーには、ハードウェア固有のドライバーのすべての操作を実行するためのコント ローラー ドライバーが用意されています。 このドライバーを使用して、SpbCx SPB コント ローラーに固有の操作を実行する通信、KMDF ドライバーが汎用的な操作を実行すると直接通信します。

SPB のコント ローラー ドライバーが通常呼び出しなど、 [ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546135) KMDF 電源イベントのコールバックと呼び出しを受信登録するメソッド、 [ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345) SPB コント ローラーから、割り込みに、ドライバーの割り込みサービス ルーチン (ISR) を接続するメソッド。 SPB 固有の操作を実行する SPB コント ローラーと通信を介して SpbCx、 [SpbCx デバイス ドライバー インターフェイス](https://msdn.microsoft.com/library/windows/hardware/hh698219)(DDI)。

SBP コント ローラー ドライバー SPB に接続されている周辺機器のデバイスの I/O 要求を処理するために使用する SpbCx と連携します。 SpbCx は、SPB コント ローラーのドライバーに共通するタスクの処理を実行します。 これらのタスクには、SPB コント ローラーの I/O 要求キューの管理が含まれます。 これらのキューには、バスに接続されている周辺機器のデバイスを管理するドライバーからの I/O 要求が含まれます。 SPB コント ローラーのドライバーは、これらの要求を処理するために必要なすべてのハードウェア固有の操作を実行します。

次の図は、SPB コント ローラーのドライバーと SpbCx を示します。

![spb コンポーネントのブロック図](images/spbmodules.png)

SPB コント ローラーのドライバーと SpbCx カーネル モードで実行して SpbCx DDI 経由で互いと通信します。 SPB コント ローラーのドライバーはドライバーに SpbCx によって実装されるサポート メソッドを呼び出します。 SpbCx は、イベント、SPB コント ローラー ドライバーによって実装されるコールバック関数を呼び出します。

SPB コント ローラーに I/O 要求を送信するドライバーは、いずれかを使用するカーネル モード ドライバー、[カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF)、またはユーザー モード ドライバーを使用する、[ユーザー モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff554928)(UMDF)。 これらのドライバーでは、読み取りを送信でき、書き込みと周辺機器の SPB 接続からデータの転送を要求することができます。 さらに、ドライバーは SPB 固有の操作を実行する I/O 制御 (IOCTL) 要求を送信できます。

SPB コント ローラーのドライバーと SPB に接続されている周辺機器のデバイスからのデータ転送を開始する SPB コント ローラー デバイスのハードウェア レジスタに直接アクセスします。 I²C など SPB、これらのデータ転送は比較的低速で発生します。 SPB コント ローラーのハードウェア レジスタはメモリ マップを使用する可能性がありますが、周辺機器のレジスタが SPB から順番にアクセスする必要があります。

SPB に接続されている周辺機器デバイス間でデータを転送する I/O 要求への応答で SPB コント ローラーのドライバーはバスの転送を開始、I/O 要求を保留中としてマークし、転送の完了を待つことがなくを返します。 その後、SPB コント ローラーのハードウェアには、転送が完了すると、コント ローラーは、割り込みを通知し、SPB コント ローラーのドライバーの ISR は保留中の I/O 要求を完了するか、要求された I/O 操作では、次の転送を開始します。

ドライバーのみ SPB コント ローラーに直接 I/O 要求を送信できます。 ときに、ユーザー モード アプリケーションにデータを転送する SPB 接続の周辺機器 SPB の周辺機器のデバイス ドライバの対応の読み取りを送信するアプリケーションが依存する必要があります。 または SPB コント ローラーへの書き込み要求。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406203" data-raw-source="[SPB Framework Extension (SpbCx)](https://msdn.microsoft.com/library/windows/hardware/hh406203)">SPB フレームワークの拡張機能 (SpbCx)</a></p></td>
<td><p>Windows 8 以降、SPB フレームワーク拡張機能 (SpbCx) がするシステム提供の拡張機能、<a href="https://msdn.microsoft.com/library/windows/hardware/ff544296" data-raw-source="[Kernel-Mode Driver Framework](https://msdn.microsoft.com/library/windows/hardware/ff544296)">カーネル モード ドライバー フレームワーク</a>(KMDF)。 SpbCx がで使用できます、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh698221" data-raw-source="[SPB controller driver](https://msdn.microsoft.com/library/windows/hardware/hh698221)">SPB コント ローラー ドライバー</a>に接続されている周辺機器のデバイスでの I/O 操作を実行する、<a href="https://msdn.microsoft.com/library/windows/hardware/hh450903" data-raw-source="[simple peripheral bus](https://msdn.microsoft.com/library/windows/hardware/hh450903)">シンプルな周辺機器のバス</a>(SPB) I²C または SPI など。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh450913" data-raw-source="[SpbCx Interfaces](https://msdn.microsoft.com/library/windows/hardware/hh450913)">SpbCx インターフェイス</a></p></td>
<td><p>SPB フレームワーク拡張機能 (SpbCx) は、2 つのインターフェイスです。 最初は、SpbCx がバスに接続されている周辺機器に SPB コント ローラーのクライアント (周辺ドライバー) を送信する I/O の要求を受け入れる、I/O 要求インターフェイスです。 2 番目のインターフェイスは、SpbCx が SPB コント ローラーのドライバーとの通信に使用するデバイス ドライバー インターフェイス (DDI) です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh450890" data-raw-source="[I/O Transfer Sequences](https://msdn.microsoft.com/library/windows/hardware/hh450890)">I/O 転送シーケンス</a></p></td>
<td><p>SPB フレームワーク拡張機能 (SpbCx) には、I/O 転送シーケンスがサポートしています。 I/O の転送シーケンスは、バスの転送 (読み取りし、書き込み操作) の順序付けされたセットがバスの単一のアトミック操作として実行します。 I/O の転送シーケンスで、転送のすべてバス上の同じターゲット デバイスにアクセスします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/jj191736" data-raw-source="[Handling Client-Implemented Sequences](https://msdn.microsoft.com/library/windows/hardware/jj191736)">クライアントで実装されたシーケンスの処理</a></p></td>
<td><p>省略可能な<a href="https://msdn.microsoft.com/library/windows/hardware/hh450814" data-raw-source="[&lt;em&gt;EvtSpbControllerLock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450814)"> <em>EvtSpbControllerLock</em> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/hh450816" data-raw-source="[&lt;em&gt;EvtSpbControllerUnlock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450816)"> <em>EvtSpbControllerUnlock</em> </a>イベント コールバック関数を補完的な実行操作です。 <em>EvtSpbControllerLock</em>関数は、ハンドラーを<a href="https://msdn.microsoft.com/library/windows/hardware/hh450858" data-raw-source="[&lt;strong&gt;IOCTL_SPB_LOCK_CONTROLLER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450858)"> <strong>IOCTL_SPB_LOCK_CONTROLLER</strong> </a>要求。 <em>EvtSpbControllerUnlock</em>関数は、ハンドラーを<a href="https://msdn.microsoft.com/library/windows/hardware/hh450859" data-raw-source="[&lt;strong&gt;IOCTL_SPB_UNLOCK_CONTROLLER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450859)"> <strong>IOCTL_SPB_UNLOCK_CONTROLLER</strong> </a>要求。 クライアント (つまり、バス上の周辺機器のデバイスのドライバー) の先頭し、末尾にこれらの要求を送信する<a href="https://msdn.microsoft.com/library/windows/hardware/hh450890" data-raw-source="[I/O transfer sequences](https://msdn.microsoft.com/library/windows/hardware/hh450890)">I/O 転送シーケンス</a>します。 ほとんどの SPB コント ローラー ドライバーがサポートしていません<strong>IOCTL_SPB_LOCK_CONTROLLER</strong>と<strong>IOCTL_SPB_UNLOCK_CONTROLLER</strong>要求と、そのため、実装しない<em>EvtSpbControllerLock</em>と<em>EvtSpbControllerUnlock</em>関数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh974776" data-raw-source="[Using the SPB_TRANSFER_LIST Structure for Custom IOCTLs](https://msdn.microsoft.com/library/windows/hardware/hh974776)">カスタム Ioctl の SPB_TRANSFER_LIST 構造体を使用します。</a></p></td>
<td><p>シンプルな周辺機器バス (SPB) コント ローラーのドライバーが 1 つをサポートまたは複数のカスタム I/O 制御 (IOCTL) を要求、使用、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh406221" data-raw-source="[&lt;strong&gt;SPB_TRANSFER_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406221)"> <strong>SPB_TRANSFER_LIST</strong> </a>読み取りについて説明し、これらのバッファーを記述する構造体要求します。 この構造体は、要求でバッファーを記述する方法を統一を示し、METHOD_BUFFERED I/O 操作に関連付けられているバッファーのコピーのオーバーヘッドを回避できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh974773" data-raw-source="[Handling IOCTL_SPB_FULL_DUPLEX Requests](https://msdn.microsoft.com/library/windows/hardware/hh974773)">IOCTL_SPB_FULL_DUPLEX 要求の処理</a></p></td>
<td><p>SPI などのいくつかのバスは、読み取りを有効にし、書き込み、バス コント ローラーと、バス上のデバイス間で同時に発生する転送。 これらの全二重転送をサポートするために、シンプルな周辺機器バス (SPB) I/O 要求インターフェイスの定義が含まれている、オプションとして、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh974774" data-raw-source="[&lt;strong&gt;IOCTL_SPB_FULL_DUPLEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh974774)"> <strong>IOCTL_SPB_FULL_DUPLEX</strong> </a> I/O 制御コード (IOCTL)。 ハードウェアの全二重の転送を実装するバス コント ローラーの SPB コント ローラー ドライバーのみをサポートする必要があります、 <strong>IOCTL_SPB_FULL_DUPLEX</strong> IOCTL します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/jj938061" data-raw-source="[How to Get the Connection Settings for a Device](https://msdn.microsoft.com/library/windows/hardware/jj938061)">デバイスの接続設定を取得する方法</a></p></td>
<td><p>SPB コント ローラーのドライバーを登録する場合、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh450818" data-raw-source="[&lt;em&gt;EvtSpbTargetConnect&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450818)"> <em>EvtSpbTargetConnect</em> </a>コールバック関数、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh406203" data-raw-source="[SPB framework extension](https://msdn.microsoft.com/library/windows/hardware/hh406203)">SPB フレームワーク拡張</a>(SpbCx) は、クライアント (ときに、この関数を呼び出す周辺機器のドライバー)、コント ローラーの送信、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff550729" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550729)"> <strong>irp_mj_create 用</strong></a>バス上のターゲット デバイスへの論理接続を開く要求。 応答、 <em>EvtSpbTargetConnect</em> SPB コント ローラーのドライバーを呼び出す必要があります、コールバック、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh450926" data-raw-source="[&lt;strong&gt;SpbTargetGetConnectionParameters&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450926)"> <strong>SpbTargetGetConnectionParameters</strong> </a>の接続を取得する方法ターゲット デバイスの設定です。 SPB コント ローラーのドライバーでは、これらの設定を格納し、それらを後でクライアントからの I/O 要求に応答内のデバイスへのアクセスに使用します。</p></td>
</tr>
</tbody>
</table>

 

 

 




