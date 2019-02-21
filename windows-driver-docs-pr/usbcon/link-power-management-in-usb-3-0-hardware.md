---
Description: This section provides information about certain limitations of the Universal Serial Bus (USB) 2.0 Selective Suspend mechanism.
title: USB 3.0 ハードウェアの電源管理のリンク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2780c8bc844d3da866e484582dbe3e798ce7a712
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559444"
---
# <a name="link-power-management-in-usb-30-hardware"></a>USB 3.0 ハードウェアの電源管理のリンク


このセクションでは、ユニバーサル シリアル バス (USB) 2.0 セレクティブ サスペンド メカニズムのいくつかの制限についての情報を提供します。 セレクティブ サスペンドと組み合わせてリンク電源管理 (LPM) を使用して USB デバイスの電源管理を実装するには、独立系ハードウェア ベンダー (Ihv) および相手先ブランド供給 (Oem) のガイドラインを示します。 また、USB コント ローラー、ハブ、およびデバイスで、LPM 実装でよくある落とし穴についての情報も提供します。 この情報は、Windows 8 およびそれ以降のバージョンに適用されます。

このセクションでは、読者が次のように慣れていることを前提とします。

-   公式[USB 3.0 仕様](http://www.usb.org/developers/docs/)します。
-   [USB セレクティブ サスペンド](https://go.microsoft.com/fwlink/p/?linkid=230964)メカニズム。 メカニズムは、ブログの投稿に記載されて[セレクティブ サスペンドの USB の分かりやすい解説](https://go.microsoft.com/fwlink/p/?linkid=230962)します。

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
<td><p><a href="limitations-of-usb-2-0-mechanism.md" data-raw-source="[Limitations of USB 2.0 Mechanism](limitations-of-usb-2-0-mechanism.md)">USB 2.0 の制限メカニズム</a></p></td>
<td><p>ユニバーサル シリアル バス (USB) 2.0 セレクティブ サスペンド メカニズムの制限事項について説明します。 USB 3.0 リンク電源管理 (LPM) 機能とそのことができますが使用方法と組み合わせてセレクティブ サスペンドのメカニズムでシステムの電力消費量を減らすの概要を示します。 最後に、USB コント ローラー、ハブ、およびデバイスで、LPM 実装でよくある落とし穴が一覧表示します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-3-0-lpm-mechanism-.md" data-raw-source="[USB 3.0 LPM Mechanism](usb-3-0-lpm-mechanism-.md)">USB 3.0 LPM メカニズム</a></p></td>
<td><p>このトピックでは、USB 3.0 LPM メカニズムについて説明します。</p>
<p>公式の補遺<a href="https://go.microsoft.com/fwlink/p/?linkid=230961" data-raw-source="[USB 2.0 Specification](https://go.microsoft.com/fwlink/p/?linkid=230961)">USB 2.0 仕様</a>(USB2_LinkPowerMangement_ECN) 新しい USB 2.0 ハードウェアに対して LPM を定義します。 このトピックでは、USB 2.0 LPM 機構は含まれません。 このトピックの目的では、具体的には U1 と U2、USB 3.0 LPM 状態について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="u1-and-u2-transitions.md" data-raw-source="[U1 and U2 Transitions](u1-and-u2-transitions.md)">U1 と U2 の遷移</a></p></td>
<td><p>このトピックには、最初は U1 および U2 の遷移を有効にするソフトウェアによって行われ、次のハードウェアでこれらの遷移が発生する方法を説明しますが、初期セットアップがについて説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="common-hardware-problems-with-u1-or-u2-implementation.md" data-raw-source="[Common Hardware Problems with U1 or U2 Implementation](common-hardware-problems-with-u1-or-u2-implementation.md)">U1 と U2 の実装、ハードウェアの一般的な問題</a></p></td>
<td><p>このトピックでは、省電力に関する LPM 機構について説明し、USB 3.0 の現在のハードウェアのさまざまな一般的な問題を説明します。 USB のあるデバイス、ハブ、およびコント ローラー U1 と U2 を正しく実装かどうか証明が必要です。 証明書の目的の準拠テストをその要件が適用されます。 (Windows 8 に含まれている) Microsoft USB ドライバー スタックは、最大電力の削減を実現するために、U1 と U2 のメカニズムを最大限に活用します。 そのためこのトピックで説明したような問題が頻繁に表示されます。 これらの問題は、ユーザー エクスペリエンスの低下につながることができ、Windows が USB 3.0 の仕様によって提供される電力の削減を実現するを防ぐことがあります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[Windows 用の USB デバイスの構築](building-usb-devices-for-windows.md)  



