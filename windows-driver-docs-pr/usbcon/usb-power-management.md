---
Description: このセクションのトピックでは、USB デバイスの電源管理のプロパティを持つ WDM power モデルが対話する方法を確認します。
title: USB クライアント ドライバーでの電源管理の実装の概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bec2d1b76c409434542eb19d1d80c65c3ef8dc0c
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67717018"
---
# <a name="overview-of-implementing-power-management-in-usb-client-drivers"></a>USB クライアント ドライバーでの電源管理の実装の概要


このセクションのトピックでは、USB デバイスの電源管理のプロパティを持つ WDM power モデルが対話する方法を確認します。

ユニバーサル シリアル バス (USB) 仕様に準拠している USB デバイスの電源管理機能には、電源管理機能のリッチで複雑なセットがあります。 これらの機能が Windows Driver Model (WDM) とやり取りする方法を理解することが重要と、システム アーキテクチャのウェイク アップをサポートするために特に機能 Microsoft Windows が標準の USB を適応させる方法。

カーネル モード ドライバー WDM 電源管理については、次を参照してください。[電源管理の実装](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-power-management)します。

USB クライアント ドライバーは、カーネル モード ドライバー フレームワーク (KMDF) に基づいており、ユーザー モード ドライバー フレームワーク (UMDF) は、基本テクノロジや USB デバイスの電源を管理するためのそれぞれのフレームワークでサポートされているメカニズムを使用する必要があります。 KMDF ベースのクライアント ドライバーでの電源を管理する方法の詳細については、次を参照してください[PnP をサポートしていると、ドライバーでの電源管理](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-pnp-and-power-management-in-your-driver); UMDF ベースのクライアント ドライバーでは、を参照してください[UMDFベースのドライバーでのPnPと電源管理](https://docs.microsoft.com/windows-hardware/drivers/wdf/pnp-and-power-management-in-umdf-drivers)。

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
<td><p><a href="comparing-usb-device-states-to-wdm-device-states.md" data-raw-source="[USB Device Power States](comparing-usb-device-states-to-wdm-device-states.md)">USB デバイスの電源の状態</a></p></td>
<td><p>このトピックでは、ユニバーサル シリアル バス 2.0 仕様のセクション 9.1 で指定された USB デバイス電源状態を使用する WDM デバイスの状態について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="selective-suspend-in-usb-drivers-wdf.md" data-raw-source="[Selective suspend in USB drivers (WDF)](selective-suspend-in-usb-drivers-wdf.md)">USB drivers (WDF) でのセレクティブ サスペンドします。</a></p></td>
<td><p>USB 関数ドライバー サポート ランタイム アイドル検出 USB のセレクティブを実装することによって中断します。 ここでは、Windows® Driver Foundation (WDF) に基づいている USB ドライバーの選択的に実装する方法についてドライバー開発者向けの中断のコンテンツします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-selective-suspend.md" data-raw-source="[USB Selective Suspend](usb-selective-suspend.md)">USB のセレクティブ サスペンドします。</a></p></td>
<td><p>このセクションでは、セレクティブ サスペンド機能の適切なメカニズムの選択についての情報を提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="register-a-composite-driver.md" data-raw-source="[How to Register a Composite Driver](register-a-composite-driver.md)">複合のドライバーを登録する方法</a></p></td>
<td><p>このトピックでは、複合のドライバーと呼ばれる、USB 多機能デバイスのドライバーを登録および基になる USB ドライバー スタックと複合デバイスの登録を解除する方法について説明します。 Microsoft 提供のドライバーで、Usbccgp.sys は、Windows によって読み込まれる既定の複合ドライバーです。 このトピックの手順では、カスタム Windows Driver Model WDM ベース複合ドライバーで、Usbccgp.sys を置換するには適用されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to--implement-remote-and-function-wake-support.md" data-raw-source="[How to Implement Function Suspend for a Composite Driver](how-to--implement-remote-and-function-wake-support.md)">複合のドライバーを中断する関数を実装する方法</a></p></td>
<td><p>このトピックでは、関数の概要が中断し、関数リモート ウェイク アップ機能ユニバーサル シリアル バス (USB) の 3.0 の多機能デバイス (複合デバイス) を提供します。 このトピックでは、ドライバーでは複合デバイスを制御するこれらの機能を実装する方法について説明します。 置換で、Usbccgp.sys 複合のドライバーをトピックが適用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="remote-wakeup-of-usb-devices.md" data-raw-source="[Remote Wakeup of USB Devices](remote-wakeup-of-usb-devices.md)">USB デバイスのリモート ウェイク アップ</a></p></td>
<td><p>このトピックでは、クライアント ドライバーでは、リモート ウェイク アップ機能を実装する方法のベスト プラクティスについて説明します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



