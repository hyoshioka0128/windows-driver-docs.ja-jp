---
title: シリアル フレームワーク拡張機能 (SerCx2) バージョン 2 の使用
description: シリアル コント ローラーを管理するシリアル フレームワーク拡張機能 (SerCx2) のバージョン 2 と連動するシリアル コント ローラー ドライバーを作成することができます。
ms.assetid: 192C25B2-936B-40D3-A0EA-5D02A234506E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edd2fcb19a17310534bbdd4759451fe45dfc479c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570802"
---
# <a name="using-version-2-of-the-serial-framework-extension-sercx2"></a>シリアル フレームワーク拡張機能 (SerCx2) バージョン 2 の使用


シリアル コント ローラーを管理するシリアル フレームワーク拡張機能 (SerCx2) のバージョン 2 と連動するシリアル コント ローラー ドライバーを作成することができます。 SerCx2 によって共同で管理されているシリアル コント ローラー上のポートに接続されている周辺機器の周辺機器のドライバーとシリアル コント ローラーのドライバーを記述することもできます。 この周辺のドライバーを使用して、[シリアルの I/O 要求インターフェイス](serial-i-o-request-interface.md)とデバイスの間のデータを転送します。 シリアル コント ローラーの拡張機能に基づく、ドライバーは、シリアルのコント ローラーのすべてのハードウェア固有のタスクの処理が、シリアル コント ローラーのすべてに共通する多くのシステム タスクを実行する SerCx2 を使用します。 SerCx2 は、Windows 8.1 以降、システム提供のコンポーネントです。

**注**  SerCx2 が Windows 8 で導入されたシリアル フレームワーク拡張機能 (SerCx) のバージョン 1 を置き換えます。 Windows 8.1 と Windows の以降のバージョンでのみ実行することを意図した新しいシリアル コント ローラー ドライバーを使用するように記述する必要があります、 [SerCx2 DDI](https://msdn.microsoft.com/library/windows/hardware/dn265349)の代わりに、 [SerCx DDI](https://msdn.microsoft.com/library/windows/hardware/dn265348)します。 ただし、Windows 8.1 と Windows の以降のバージョンは、SerCx DDI を使用する既存のコント ローラーのシリアル ドライバーをサポートします。

 

シリアル コント ローラーは、互換性のあるデバイスまたは 16550 ユニバーサル非同期受信側/送信元 (UART) です。 詳細については、[シリアル コント ローラーのドライバーの概要](serial-drivers-overview.md)を参照してください。

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
<td><p><a href="sercx2-architectural-overview.md" data-raw-source="[SerCx2 Architectural Overview](sercx2-architectural-overview.md)">SerCx2 アーキテクチャの概要</a></p></td>
<td><p>SerCx2 は周辺機器のドライバーと逐次的に接続されている周辺機器のデバイス間の通信を有効にするシリアル コント ローラー ドライバーと共に動作します。 通常、シリアル コント ローラーは SoC チップの外部にあるが、同じプリント回路基板をはんだ付けは周辺機器のデバイスとのピン数の少ない通信を提供するには、チップ (SoC) チップをシステムに統合します。</p></td>
</tr>
<tr class="even">
<td><p><a href="serial-controller-driver-design-for-sercx2.md" data-raw-source="[Serial Controller Driver Design for SerCx2](serial-controller-driver-design-for-sercx2.md)">SerCx2 のコント ローラーのシリアル ドライバーの設計</a></p></td>
<td><p>シリアル、コント ローラーを管理するには、ハードウェアに固有のタスクを実行し、SerCx2 と通信するシリアル コント ローラー ドライバーを作成します。 Windows 8.1 以降、SerCx2 は、シリアル コント ローラーに共通する処理タスクの多くを処理するシステム提供のコンポーネントです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="accessing-a-device-on-a-sercx2-managed-serial-port.md" data-raw-source="[Accessing a Device on a SerCx2-Managed Serial Port](accessing-a-device-on-a-sercx2-managed-serial-port.md)">SerCx2 で管理されたシリアル ポート上のデバイスへのアクセス</a></p></td>
<td><p>SerCx2 とコント ローラーのシリアル ドライバーの周辺機器が完全に接続されているシリアル ポートを連携して管理します。 SerCx2 で管理されたシリアル ポート周辺機器にアクセスするには、周辺機器は、ドライバーは、シリアル ポートへの論理接続を開きをこの接続を表すファイル ハンドルを取得します。 ドライバーは、I/O 要求をポートに送信するのにこのハンドルを使用します。</p></td>
</tr>
</tbody>
</table>

 

 

 




