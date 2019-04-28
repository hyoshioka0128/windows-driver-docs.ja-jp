---
title: USB 2.0 の拡張機能
description: このセクションでは、USB 2.0 デバッガー拡張機能のコマンドについて説明します。 これらのコマンドは、USB 2.0 ドライバー スタックのドライバーによって管理されるデータ構造から情報を表示します。
ms.assetid: 42A78738-CE0D-42EA-9E3D-04CDC2060266
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b506fe76da4e30b53a5c220b3b2d0e5a85caafa2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367990"
---
# <a name="usb-20-extensions"></a>USB 2.0 の拡張機能


このセクションでは、USB 2.0 デバッガー拡張機能のコマンドについて説明します。 これらのコマンドは、USB 2.0 ドライバー スタックのドライバーによって管理されるデータ構造から情報を表示します。 これら 3 つのドライバーの詳細については、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkId=251983)します。

USB 2.0 デバッガー拡張機能のコマンドは、Usbkd.dll で実装されます。 Usbkd コマンドを読み込むには、次のように入力します。 **.load usbkd.dll**デバッガーでします。

## <a name="span-idusb-2-treespanspan-idusb2treespanusb-20-tree"></a><span id="usb-2-tree"></span><span id="USB_2_TREE"></span>USB 2.0 ツリー


USB 2.0 ツリーには、ハブを表す子ノードと共に EHCI ホスト コント ローラーのデバイスと接続されているデバイスでの実行単位を表すデバイス ノードが含まれています。 この図では、USB 2.0 ツリーの例を示します。

![usb 2tree を示す図](images/usbkd01.png)

図には、1 つの物理ホスト コント ローラーのデバイスを持つ 2 つの実行単位を示します。 各実行の単位は、プラグ アンド プレイ デバイス ツリー内のデバイス ノードとして表示されます。 1 つの実行単位が UHCI USB ホスト コント ローラーのノードとして表示され、EHCI USB ホスト コント ローラー ノードとその他の実行単位を示しています。 これらのノードのそれぞれは、USB ルート ハブを表す子ノードがあります。 各ルート ハブでは、接続された USB デバイスを表す 1 つの子ノードを持ちます。

ダイアグラムがないすべてのノードが 1 つの親ノードから派生したという意味でのツリーではないことに注意してください。 ただし、用語を使用しました*USB 2.0 ツリー*ハブのノードだけでなく EHCI ホスト コント ローラー デバイスと接続されているデバイスでの実行単位を表すデバイス ノードのセットについて言及しています。

## <a name="span-idgettingstartedwithusb20debuggingspanspan-idgettingstartedwithusb20debuggingspangetting-started-with-usb-20-debugging"></a><span id="getting_started_with_usb_2.0_debugging"></span><span id="GETTING_STARTED_WITH_USB_2.0_DEBUGGING"></span>USB 2.0 の概要のデバッグ


USB 2.0 の問題のデバッグを開始するには、入力、 [ **! usb2tree** ](-usbkd-usb2tree.md)コマンド。 **! Usb2tree**コマンドは、コマンドとホスト コント ローラー、ハブ、ポート、デバイス、エンドポイント、および USB 2.0 ツリーの他の要素を調査するために使用できるアドレスの一覧を表示します。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [**!usbkd.usbhelp**](-usbkd-usbhelp.md)
-   [**!usbkd.\_ehcidd**](-usbkd--ehcidd.md)
-   [**!usbkd.\_ehciep**](-usbkd--ehciep.md)
-   [**!usbkd.\_ehciframe**](-usbkd--ehciframe.md)
-   [**!usbkd.\_ehciqh**](-usbkd--ehciqh.md)
-   [**! usbkd します。\_ehciregs**](-usbkd--ehciregs.md)
-   [**! usbkd します。\_ehcisitd**](-usbkd--ehcisitd.md)
-   [**!usbkd.\_ehcistq**](-usbkd--ehcistq.md)
-   [**! usbkd します。\_ehcitd**](-usbkd--ehcitd.md)
-   [**! usbkd します。\_ehcitfer**](-usbkd--ehcitfer.md)
-   [**! usbkd します。\_ehciitd**](-usbkd--ehciitd.md)
-   [**!usbkd.doesdumphaveusbdata**](-usbkd-doesdumphaveusbdata.md)
-   [**!usbkd.isthisdumpasyncissue**](-usbkd-isthisdumpasyncissue.md)
-   [**!usbkd.urbfunc**](-usbkd-urbfunc.md)
-   [**!usbkd.usb2**](-usbkd-usb2.md)
-   [**!usbkd.usb2tree**](-usbkd-usb2tree.md)
-   [**!usbkd.usbchain**](-usbkd-usbchain.md)
-   [**!usbkd.usbdevobj**](-usbkd-usbdevobj.md)
-   [**!usbkd.usbdpc**](-usbkd-usbdpc.md)
-   [**!usbkd.ehci\_info\_from\_fdo**](-usbkd-ehci-info-from-fdo.md)
-   [**!usbkd.usbdevh**](-usbkd-usbdevh.md)
-   [**!usbkd.usbep**](-usbkd-usbep.md)
-   [**!usbkd.usbfaildata**](-usbkd-usbfaildata.md)
-   [**!usbkd.usbhcdext**](-usbkd-usbhcdext.md)
-   [**!usbkd.usbdstatus**](-usbkd-usbdstatus.md)
-   [**!usbkd.usbhcdhccontext**](-usbkd-usbhcdhccontext.md)
-   [**!usbkd.usbhcdlist**](-usbkd-usbhcdlist.md)
-   [**!usbkd.usbhcdlistlogs**](-usbkd-usbhcdlistlogs.md)
-   [**!usbkd.usbhcdlog**](-usbkd-usbhcdlog.md)
-   [**!usbkd.usbhcdlogex**](-usbkd-usbhcdlogex.md)
-   [**!usbkd.usbhcdpnp**](-usbkd-usbhcdpnp.md)
-   [**!usbkd.usbhcdpow**](-usbkd-usbhcdpow.md)
-   [**!usbkd.hub2\_info\_from\_fdo**](-usbkd-hub2-info-from-fdo.md)
-   [**!usbkd.usbhuberr**](-usbkd-usbhuberr.md)
-   [**!usbkd.usbhubext**](-usbkd-usbhubext.md)
-   [**!usbkd.usbhubinfo**](-usbkd-usbhubinfo.md)
-   [**!usbkd.usbhublog**](-usbkd-usbhublog.md)
-   [**!usbkd.usbhubmddevext**](-usbkd-usbhubmddevext.md)
-   [**!usbkd.usbhubmdpd**](-usbkd-usbhubmdpd.md)
-   [**!usbkd.usbhubpd**](-usbkd-usbhubpd.md)
-   [**!usbkd.usbhubs**](-usbkd-usbhubs.md)
-   [**!usbkd.usblist**](-usbkd-usblist.md)
-   [**!usbkd.usbpo**](-usbkd-usbpo.md)
-   [**!usbkd.usbpdos**](-usbkd-usbpdos.md)
-   [**!usbkd.usbpdoxls**](-usbkd-usbpdoxls.md)
-   [**!usbkd.usbpnp**](-usbkd-usbpnp.md)
-   [**!usbkd.usbportisasyncadv**](-usbkd-usbportisasyncadv.md)
-   [**!usbkd.usbportmdportlog**](-usbkd-usbportmdportlog.md)
-   [**!usbkd.usbportmddcontext**](-usbkd-usbportmddcontext.md)
-   [**!usbkd.usbportmddevext**](-usbkd-usbportmddevext.md)
-   [**!usbkd.usbtriage**](-usbkd-usbtriage.md)
-   [**!usbkd.usbtt**](-usbkd-usbtt.md)
-   [**!usbkd.usbtx**](-usbkd-usbtx.md)
-   [**!usbkd.usbusb2ep**](-usbkd-usbusb2ep.md)
-   [**!usbkd.usbusb2tt**](-usbkd-usbusb2tt.md)
-   [**!usbkd.usbver**](-usbkd-usbver.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[USB 3.0 の拡張機能](usb-3-extensions.md)

[RCDRKD 拡張機能](rcdrkd-extensions.md)

 

 






