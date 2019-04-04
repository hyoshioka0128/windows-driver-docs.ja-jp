---
title: 電源状態の機能をサポートしています。
description: 電源状態の機能をサポートしています。
ms.assetid: F96214C9-702D-402E-B873-5DF57C521B34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b35c98b3faa551fbdf954c2d2a6ee0d9a24d5ca4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539547"
---
# <a name="supporting-functional-power-states"></a>電源状態の機能をサポートしています。


Windows 8 以降、電源マネージャーには、実行時の電源管理フレームワーク (PoFx) が含まれています。 PoFx では、コンポーネント (またはサブデバイス) レベルでの電源とクロックの管理をサポートします。

KMDF バージョン 1.11 以降、KMDF ドライバーを利用できます PoFx を提供する詳細な電源管理の。 具体的には、KMDF ドライバーでは、それぞれが個別にできます電源管理の対象を 1 つのデバイス内の複数の論理コンポーネントを定義できます。

たとえば、関数ドライバーは一意のデバイスの論理コンポーネントで各機能の電源状態のセットを定義する可能性があります。 デバイスとシステムの電源状態と同様に、F0 ことを示しますコンポーネントが完全に中は、省略可能な状態ながら F1、f2 キーには、段階的に低電力状態を示します。 [Fx] の状態をサポートするには、ドライバーは、デバイスの電源ポリシー所有者にある必要があります。

次の表は、さまざまな機能の電源状態のシナリオのフレームワークのサポートをまとめたものです。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">種類</th>
<th align="left">KMDF サポート</th>
<th align="left">UMDF サポート</th>
<th align="left">使用方法を実装する場合</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-single-component-devices.md" data-raw-source="[Single component, single state (F0)](supporting-multiple-functional-power-states-for-single-component-devices.md)">1 つのコンポーネント、1 つの状態 (F0)</a></p></td>
<td align="left"><p>サポート対象</p></td>
<td align="left"><p>サポート対象</p></td>
<td align="left"><p>電源エンジン プラグイン (PEP) をアイドル タイムアウト値を判断して、ドライバーが 1 つだけの F 状態。</p>
<p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff545903" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545903)"> <strong>WdfDeviceAssignS0IdleSettings</strong> </a>で<em>IdleTimeoutType</em> = <strong>SystemManagedIdleTimout</strong>または<strong>SystemManagedIdleTimoutWithHint</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-single-component-devices.md" data-raw-source="[Single component, multiple states (F0, F1, F2…)](supporting-multiple-functional-power-states-for-single-component-devices.md)">1 つのコンポーネントでは、複数の状態 (F0、F1、F2...)</a></p></td>
<td align="left"><p>サポート対象</p></td>
<td align="left"><p>サポートされない</p></td>
<td align="left"><p>ドライバーは、1 つ以上の F 状態が場合。</p>
<ul>
<li>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/hh451097" data-raw-source="[&lt;strong&gt;WdfDeviceWdmAssignPowerFrameworkSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451097)"> <strong>WdfDeviceWdmAssignPowerFrameworkSettings</strong> </a> WDM PoFx コールバックを登録します。</li>
<li>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff545903" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545903)"> <strong>WdfDeviceAssignS0IdleSettings</strong> </a>で<em>IdleTimeoutType</em> = <strong>SystemManagedIdleTimout</strong>します。</li>
</ul>
<p>この場合は、KMDF、PoFx やり取りのほとんどを処理します。</p>
<p>サンプル コードでは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=617937" data-raw-source="[PoFx sample drivers](https://go.microsoft.com/fwlink/p/?LinkId=617937)">PoFx サンプル ドライバー</a>を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-multiple-component-devices.md" data-raw-source="[Multiple components, single or multiple states](supporting-multiple-functional-power-states-for-multiple-component-devices.md)">複数のコンポーネント、1 つまたは複数の状態</a></p></td>
<td align="left"><p>WDM インターフェイスを使用してサポートされています。</p></td>
<td align="left"><p>サポートされない</p></td>
<td align="left"><p>ドライバーは、複数のコンポーネントが場合。 この場合、PoFx インターフェイスを直接使用する必要があります。</p>
<p>サンプル コードでは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=617937" data-raw-source="[PoFx sample drivers](https://go.microsoft.com/fwlink/p/?LinkId=617937)">PoFx サンプル ドライバー</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

KMDF PoFx 上に最小限の抽象化を追加するためには、ドライバーを記述する前に PoFx の基本を理解することをお勧めします。 確認すること勧めその結果、 [、電源管理フレームワークの概要](https://msdn.microsoft.com/library/windows/hardware/hh406637)これらのトピックを読む前にします。

 

 





