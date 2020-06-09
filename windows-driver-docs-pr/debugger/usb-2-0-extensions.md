---
title: USB 2.0 拡張機能
description: ここでは、USB 2.0 デバッガー拡張機能のコマンドについて説明します。 これらのコマンドは、ドライバーによって管理されているデータ構造の情報を USB 2.0 ドライバースタックに表示します。
ms.assetid: 42A78738-CE0D-42EA-9E3D-04CDC2060266
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95e4888ff5af72e4778213adc1d69b3a325f2830
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533834"
---
# <a name="usb-20-extensions"></a>USB 2.0 拡張機能

ここでは、USB 2.0 デバッガー拡張機能のコマンドについて説明します。 これらのコマンドは、ドライバーによって管理されているデータ構造の情報を USB 2.0 ドライバースタックに表示します。 これら3つのドライバーの詳細については、「 [Windows の USB ホスト側ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

USB 2.0 デバッガー拡張コマンドは、Usbkd .dll に実装されています。 Usbkd コマンドを読み込むには、デバッガーで「」と入力します **。**

## <a name="span-idusb-2-treespan-usb-20-tree"></a><span id="usb-2-tree"></span>USB 2.0 ツリー

USB 2.0 ツリーには、EHCI ホストコントローラーデバイス上の実行単位を表すデバイスノードと、ハブと接続されているデバイスを表す子ノードが含まれています。 次の図は、USB 2.0 ツリーの例を示しています。

![usb 2tree を示す図](images/usbkd01.png)

この図は、2つの実行ユニットを持つ1つの物理ホストコントローラーデバイスを示しています。 各実行単位は、デバイスノードとしてプラグアンドプレイデバイスツリーに表示されます。 1つの実行単位が UHCI USB ホストコントローラーノードとして表示され、もう一方の実行単位は EHCI USB ホストコントローラーノードとして表示されます。 これらの各ノードには、USB ルートハブを表す子ノードがあります。 各ルートハブには、接続された USB デバイスを表す1つの子ノードがあります。

図はツリーではなく、すべてのノードが1つの親ノードからのものではないことに注意してください。 ただし、 *USB 2.0 ツリー*という用語を使用する場合、ここでは、EHCI ホストコントローラーデバイス上の実行単位を表すデバイスノードのセットと、ハブおよび接続されているデバイスのノードを参照します。

## <a name="getting-started-with-usb-20-debugging"></a>USB 2.0 デバッグの概要


USB 2.0 の問題のデバッグを開始するには、 [**! usb2tree**](-usbkd-usb2tree.md)コマンドを入力します。 **! Usb2tree**コマンドは、ホストコントローラー、ハブ、ポート、デバイス、エンドポイント、および USB 2.0 ツリーのその他の要素を調査するために使用できるコマンドとアドレスの一覧を表示します。

## <a name="in-this-section"></a>このセクションの内容


-   [**!usbkd.usbhelp**](-usbkd-usbhelp.md)
-   [**! usbkd。 \_ehcidd**](-usbkd--ehcidd.md)
-   [**! usbkd。 \_ehciep**](-usbkd--ehciep.md)
-   [**! usbkd。 \_ehciframe**](-usbkd--ehciframe.md)
-   [**! usbkd。 \_ehciqh**](-usbkd--ehciqh.md)
-   [**! usbkd。 \_ehciregs**](-usbkd--ehciregs.md)
-   [**! usbkd。 \_ehcisitd**](-usbkd--ehcisitd.md)
-   [**! usbkd。 \_ehcistq**](-usbkd--ehcistq.md)
-   [**! usbkd。 \_ehcitd**](-usbkd--ehcitd.md)
-   [**! usbkd。 \_ehcitfer**](-usbkd--ehcitfer.md)
-   [**! usbkd。 \_ehciitd**](-usbkd--ehciitd.md)
-   [**!usbkd.doesdumphaveusbdata**](-usbkd-doesdumphaveusbdata.md)
-   [**!usbkd.isthisdumpasyncissue**](-usbkd-isthisdumpasyncissue.md)
-   [**!usbkd.urbfunc**](-usbkd-urbfunc.md)
-   [**!usbkd.usb2**](-usbkd-usb2.md)
-   [**!usbkd.usb2tree**](-usbkd-usb2tree.md)
-   [**!usbkd.usbchain**](-usbkd-usbchain.md)
-   [**!usbkd.usbdevobj**](-usbkd-usbdevobj.md)
-   [**!usbkd.usbdpc**](-usbkd-usbdpc.md)
-   [**! usbkd. \_ \_ fdo からの ehci 情報 \_**](-usbkd-ehci-info-from-fdo.md)
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
-   [**! usbkd. hub2 \_ info \_ from \_ fdo**](-usbkd-hub2-info-from-fdo.md)
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

## <a name="related-topics"></a>関連トピック

[USB 3.0 拡張機能](usb-3-extensions.md)

[RCDRKD 拡張機能](rcdrkd-extensions.md)
