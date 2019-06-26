---
title: 汎用 I/O (GPIO) ドライバーの設計ガイド
description: このセクションでは、汎用 I/O (GPIO) コントローラー デバイスのドライバーを記述する方法について説明します。
ms.assetid: D11E72AC-2B0D-4325-8BD0-9AE9B21AFD8D
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 48ec0635c4fc9ea71145550e63cc9012f3efe8db
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393104"
---
# <a name="general-purpose-io-gpio-driver-design-guide"></a>汎用 I/O (GPIO) ドライバーの設計ガイド


このセクションでは、汎用 I/O (GPIO) コントローラー デバイスのドライバーを記述する方法について説明します。 GPIO コントローラーでは、低速のデータ I/O 操作を実行し、デバイス選択として機能し、割り込み要求を受信するよう GPIO ピンが構成されます。 Windows 8 以降では、GPIO フレームワーク拡張機能 (GpioClx) により、GPIO コントローラー用のドライバーを記述するタスクが簡略化されます。 さらに、GpioClx により、コントローラー上の GPIO ピンに接続されるデバイスと通信する周辺機器のドライバーに対して、統一された I/O 要求インターフェイスが提供されます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview" data-raw-source="[GPIO Driver Support Overview](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)">GPIO ドライバー サポートの概要</a></p></td>
<td><p>Windows 8 以降では、GPIO フレームワーク拡張機能 (GpioClx) により、GPIO コントローラー デバイス用のドライバーを記述するタスクが簡略化されます。 さらに、GpioClx により、GPIO ピンに接続される周辺機器に対してドライバー サポートが提供されます。 カーネル モード ドライバー フレームワーク (KMDF) のシステム提供の拡張機能である GpioClx では、GPIO デバイス クラスのメンバーに共通す処理タスクが実行されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpioclx-i-o-and-interrupt-interfaces" data-raw-source="[GpioClx I/O and Interrupt Interfaces](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpioclx-i-o-and-interrupt-interfaces)">GpioClx I/O と割り込みインターフェイス</a></p></td>
<td><p>通常、GPIO コントローラーのクライアントは、GPIO ピンに接続される周辺機器のドライバーです。 これらのドライバーでは、低帯域幅のデータ チャネル、デバイス選択の出力、および割り込み要求の入力として GPIO ピンが使用されます。 周辺機器のドライバーにより、データ入力またはデータ出力として構成されている GPIO ピンへの論理接続が開かれます。 これらの接続を使用して、これらのピンに I/O 要求が送信されます。 さらに、周辺機器のドライバーでは、割り込み要求の入力として構成されている GPIO ピンに、割り込みサービス ルーチンを論理的に接続できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-based-hardware-resources" data-raw-source="[GPIO-Based Hardware Resources](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-based-hardware-resources)">GPIO ベースのハードウェア リソース</a></p></td>
<td><p>Windows 8 以降では、GPIO コントローラーのドライバーによって制御される汎用 I/O (GPIO) ピンは、システムで管理されるハードウェア リソースとして他のドライバーで使用できます。 データ入力またはデータ出力として構成されているピンである GPIO I/O ピンは、新しい種類の Windows リソースである <em>GPIO I/O リソース</em>として使用できます。 さらに、割り込み要求の入力として構成されているピンである GPIO 割り込みピンは、通常の Windows 割り込みリソースとして使用できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts" data-raw-source="[GPIO Interrupts](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)">GPIO 割り込み</a></p></td>
<td><p>一部の汎用 I/O (GPIO) コントローラー デバイスでは、割り込み要求の入力として機能するよう GPIO ピンを構成できます。 これらの割り込み要求の入力は、GPIO ピンに物理的に接続されている周辺機器によって駆動されます。 これらの GPIO コントローラー用のドライバーにより、個々の GPIO ピンで割り込み要求の有効化、無効化、マスク、マスク解除、およびクリアを実行できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpioclx-ddi" data-raw-source="[GpioClx DDI](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpioclx-ddi)">GpioClx DDI</a></p></td>
<td><p>汎用 I/O (GPIO) コントローラーのドライバーは、GpioClx デバイス ドライバー インターフェイス (DDI) を介して GPIO フレームワーク拡張機能 (GpioClx) と通信します。 この DDI は Gpioclx.h ヘッダー ファイルで定義され、<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index" data-raw-source="[General-Purpose I/O (GPIO) Driver Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)">汎用 I/O (GPIO) ドライバー リファレンス</a>に記載されています。 この DDI の一部として、GpioClx により、GPIO コントローラーのドライバーによって呼び出されるいくつかの<a href="https://docs.microsoft.com/previous-versions/hh439460(v=vs.85)" data-raw-source="[driver support methods](https://docs.microsoft.com/previous-versions/hh439460(v=vs.85))">ドライバー サポート メソッド</a>が実装されます。 このドライバーにより、GpioClx によって呼び出される一連の<a href="https://docs.microsoft.com/previous-versions/hh439464(v=vs.85)" data-raw-source="[event callback functions](https://docs.microsoft.com/previous-versions/hh439464(v=vs.85))">イベント コールバック関数</a>が実装されます。 GpioClx では、これらのコールバックを使用して、割り込みの入力として構成されている GPIO ピンからの割り込み要求が管理され、データ入力およびデータ出力として構成されている GPIO ピンとの間でデータ転送が行われます。</p></td>
</tr>
</tbody>
</table>

 

 

 




