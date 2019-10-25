---
title: 機能電源状態のサポート
description: 機能電源状態のサポート
ms.assetid: F96214C9-702D-402E-B873-5DF57C521B34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a551255747202404e10beb02d7a49c99e96dcd27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831799"
---
# <a name="supporting-functional-power-states"></a>機能電源状態のサポート


Windows 8 以降では、power manager にはランタイム電源管理フレームワーク (PoFx) が含まれています。 PoFx は、コンポーネント (またはサブデバイス) レベルでの電源とクロックの管理をサポートしています。

Kmdf バージョン1.11 以降、KMDF ドライバーは、PoFx によって提供される詳細な電源管理機能を利用できます。 特に、KMDF ドライバーでは、1つのデバイス内に複数の論理コンポーネントを定義できます。これらはそれぞれ独立した電源管理を行うことができます。

たとえば、関数ドライバーでは、デバイスの各論理コンポーネントに対して、機能的な電源状態の一意のセットを定義できます。 デバイスとシステムの電源状態と同様、F0 はコンポーネントが完全にオンになっていることを示し、オプションの状態 F1、F2 などは、徐々に低い電力状態を示します。 Fx の状態をサポートするには、ドライバーがデバイスの電源ポリシーの所有者である必要があります。

次の表は、さまざまな機能の電源状態のシナリオに対するフレームワークのサポートをまとめたものです。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">タスクバーの検索ボックスに</th>
<th align="left">KMDF のサポート</th>
<th align="left">UMDF サポート</th>
<th align="left">使用するタイミング/実装方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-single-component-devices.md" data-raw-source="[Single component, single state (F0)](supporting-multiple-functional-power-states-for-single-component-devices.md)">単一コンポーネント、単一状態 (F0)</a></p></td>
<td align="left"><p>サポートされる</p></td>
<td align="left"><p>サポートされる</p></td>
<td align="left"><p>電源エンジンプラグイン (PEP) を使用してアイドルタイムアウト値を決定し、ドライバーに1つだけの F 状態がある場合。</p>
<p><em>IdleTimeoutType</em> = <strong>SystemManagedIdleTimout</strong>または<strong>SystemManagedIdleTimoutWithHint</strong>を使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)"><strong>WdfDeviceAssignS0IdleSettings</strong></a>を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-single-component-devices.md" data-raw-source="[Single component, multiple states (F0, F1, F2…)](supporting-multiple-functional-power-states-for-single-component-devices.md)">単一コンポーネント、複数の状態 (F0、F1、F2...)</a></p></td>
<td align="left"><p>サポートされる</p></td>
<td align="left"><p>サポートされない</p></td>
<td align="left"><p>ドライバーに複数の F 状態がある場合。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings" data-raw-source="[&lt;strong&gt;WdfDeviceWdmAssignPowerFrameworkSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)"><strong>Wdfdevicewdm割り当て Powerframeworksettings</strong></a>を呼び出して、WDM pofx コールバックを登録します。</li>
<li><em>IdleTimeoutType</em> = <strong>SystemManagedIdleTimout</strong>を使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)"><strong>WdfDeviceAssignS0IdleSettings</strong></a>を呼び出します。</li>
</ul>
<p>この場合、KMDF は PoFx とのほとんどのやり取りを処理します。</p>
<p>サンプルコードについては、「 <a href="https://go.microsoft.com/fwlink/p/?LinkId=617937" data-raw-source="[PoFx sample drivers](https://go.microsoft.com/fwlink/p/?LinkId=617937)">Pofx サンプルドライバー</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-multiple-component-devices.md" data-raw-source="[Multiple components, single or multiple states](supporting-multiple-functional-power-states-for-multiple-component-devices.md)">複数のコンポーネント、1つまたは複数の状態</a></p></td>
<td align="left"><p>サポート (WDM インターフェイスを使用)</p></td>
<td align="left"><p>サポートされない</p></td>
<td align="left"><p>ドライバーに複数のコンポーネントがある場合。 この場合は、PoFx インターフェイスを直接使用する必要があります。</p>
<p>サンプルコードについては、「 <a href="https://go.microsoft.com/fwlink/p/?LinkId=617937" data-raw-source="[PoFx sample drivers](https://go.microsoft.com/fwlink/p/?LinkId=617937)">Pofx サンプルドライバー</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

KMDF では、PoFx の上に最小限の抽象化が追加されるため、ドライバーを記述する前に、PoFx に関する基本的な知識があることをお勧めします。 そのため、これらのトピックを読む前に、 [「電源管理フレームワークの概要」](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)をお読みになることをお勧めします。

 

 





