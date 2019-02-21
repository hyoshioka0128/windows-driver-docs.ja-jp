---
title: GPIO 割り込み
description: 汎用入出力 (GPIO) コント ローラー デバイスによっては、割り込み要求の入力として機能するには、その GPIO ピンを構成できます。
ms.assetid: 0F56AD4C-E0BF-49F1-AB67-0107D08DEF9F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5caf6df9af8a5e6991ccf9154b79f27cffb407be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537810"
---
# <a name="gpio-interrupts"></a>GPIO 割り込み


汎用入出力 (GPIO) コント ローラー デバイスによっては、割り込み要求の入力として機能するには、その GPIO ピンを構成できます。 これらの割り込み要求入力については、GPIO ピンに物理的に接続されている周辺機器によって決まります。 これらの GPIO コント ローラー用ドライバーできますを有効にするを無効にする、マスク、マスク解除、および個々 の GPIO ピンの割り込み要求をオフにします。

GPIO 割り込みのサポートは、省略可能です。 GPIO フレームワーク拡張機能 (GpioClx) では、GPIO 割り込みをサポートするために GPIO コント ローラーは必要ありません。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698263" data-raw-source="[Primary and Secondary Interrupts](https://msdn.microsoft.com/library/windows/hardware/hh698263)">プライマリとセカンダリの割り込み</a></p></td>
<td><p>GPIO 割り込み処理が 2 段階のプロセスでは本質的にします。 GPIO フレームワーク拡張機能 (GpioClx) 割り込みサービス ルーチン (ISR) を実行するとの汎用的な I/O (GPIO) コントローラからの割り込みと呼ばれる、<em>プライマリ割り込み</em>します。 この ISR では、グローバル システムの割り込み (GSI) に割り込む GPIO ピンをマップし、ハードウェア アブストラクション レイヤー (HAL) にこの GSI を渡します。 HAL を生成、<em>セカンダリ割り込み</em>を通じてこの GSI GPIO ピンに論理的に接続されている 2 つ目の ISR を実行します。 このプロセスはダイアグラムに示した<a href="https://msdn.microsoft.com/library/windows/hardware/hh439512#gpio-block-diagram" data-raw-source="[GPIO Driver Support Overview](https://msdn.microsoft.com/library/windows/hardware/hh439512#gpio-block-diagram)">GPIO ドライバー サポートの概要</a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698246" data-raw-source="[GPIO-Based Interrupt Resources](https://msdn.microsoft.com/library/windows/hardware/hh698246)">割り込みの GPIO ベースのリソース</a></p></td>
<td><p>割り込みを汎用入出力 (GPIO) ピンとして抽象 Windows GPIO 割り込みを取得する送信周辺機器のデバイス用のドライバーでは、リソースを中断します。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff544296" data-raw-source="[Kernel-mode driver framework](https://msdn.microsoft.com/library/windows/hardware/ff544296)">カーネル モード ドライバー フレームワーク</a>(KMDF) ドライバーを通じてこれらのリソースが表示される、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"> <em>EvtDevicePrepareHardware</em> </a>イベント コールバック関数。 </p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698262" data-raw-source="[Passive-Level ISRs](https://msdn.microsoft.com/library/windows/hardware/hh698262)">パッシブ レベル isr を特定します。</a></p></td>
<td><p>Windows 8、カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) ドライバーを開始できます、オプションとして、登録、割り込みサービス ルーチン (Isr) パッシブ レベルで実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698260" data-raw-source="[Interrupt-Related Callbacks](https://msdn.microsoft.com/library/windows/hardware/hh698260)">割り込みに関連するコールバック</a></p></td>
<td><p>オプションとして、汎用入出力 (GPIO) コント ローラーのドライバーは、GPIO 割り込みのサポートを提供できます。 GPIO 割り込みをサポートするためには、GPIO コント ローラーのドライバーは、これらの割り込みを管理するコールバック関数のセットを実装します。 ドライバーには、GPIO フレームワークの拡張機能 (GpioClx) のクライアントとして自身を登録するときに、ドライバーが提供する登録パケット内のこれらのコールバック関数へのポインターが含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/jj851070" data-raw-source="[Interrupt Synchronization for GPIO Controller Drivers](https://msdn.microsoft.com/library/windows/hardware/jj851070)">GPIO コント ローラーのドライバーの同期を中断します。</a></p></td>
<td><p>GPIO コント ローラー ドライバーが呼び出すことができます、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh439482" data-raw-source="[&lt;strong&gt;GPIO_CLX_AcquireInterruptLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439482)"> <strong>GPIO_CLX_AcquireInterruptLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/hh439494" data-raw-source="[&lt;strong&gt;GPIO_CLX_ReleaseInterruptLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439494)"> <strong>GPIO_CLX_ReleaseInterruptLock</strong> </a>メソッド取得および GPIO フレームワーク拡張機能 (GpioClx) によって内部的に実装される割り込みロックを解放します。 IRQL で実行されるドライバー コード = PASSIVE_LEVEL GpioClx で割り込みサービス ルーチン (ISR) に同期するこれらのメソッドを呼び出すことができます。 GpioClx 専用に GPIO コント ローラーのピンの各銀行に別の割り込みロックします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698245" data-raw-source="[Enabling and Disabling Shared GPIO Interrupts](https://msdn.microsoft.com/library/windows/hardware/hh698245)">共有 GPIO 割り込みを有効化と無効化</a></p></td>
<td><p>場合によっては、2 つ以上の周辺機器からの割り込み要求行が同じ物理汎用入出力 (GPIO) ピンに接続します。 共有の割り込みの行の GPIO ピンは通常、割り込みのトリガーされたレベルの構成します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698251" data-raw-source="[GPIO Interrupt Masks](https://msdn.microsoft.com/library/windows/hardware/hh698251)">GPIO 割り込みマスク</a></p></td>
<td><p>割り込み入力はマスクやほかにマスク解除が有効と無効にできるように構成されている汎用の I/O (GPIO) ピンです。</p></td>
</tr>
</tbody>
</table>

 

 

 




