---
title: xhci_dumpall usb3kd
description: Usb3kd コマンドは、コンピューター上のすべての USB 3.0 ホストコントローラーに関する情報を表示します xhci_dumpall。 表示は、UsbXhci によって管理されるデータ構造に基づいています。
ms.assetid: D1087DC6-B065-48E3-93B2-EF53AE9DA8C7
keywords:
- usb3kd Windows デバッグの xhci_dumpall
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_dumpall
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bcb79bc5ee5cd41d12d1e835f3d4a0b65f5a97ac
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534893"
---
# <a name="usb3kdxhci_dumpall"></a>! usb3kd xhci \_ dumpall


[**! Usb3kd. xhci \_ dumpall**](-usb3kd-device-info.md)コマンドは、コンピューター上のすべての USB 3.0 ホストコントローラーに関する情報を表示します。 この表示は、USB 3.0 ホストコントローラードライバー (UsbXhci) によって管理されているデータ構造に基づいています。

```dbgcmd
!usb3kd.xhci_dumpall [1]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_____________1"></span> **1**  
すべての XHCI コマンドを実行し、各コマンドの出力を表示します。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


次のスクリーンショットは、 **! xhci \_ dumpall**l コマンドの出力を示しています。

![\-xhci controller 情報を示す! xhci dumpall コマンドの出力](images/xhcidumpall01.png)

出力には、USB 3.0 ホストコントローラーが1つあることが示されています。

出力では、[デバッガーマークアップ言語 (DML) を使用して](debugger-markup-language-commands.md)リンクを提供します。 これらのリンクは、USB 3.0 ホストコントローラードライバーによって管理されているホストコントローラーの状態に関する詳細情報を提供するコマンドを実行します。 たとえば、[ [**! xhci \_ 機能**](-usb3kd-xhci-capability.md)] リンクをクリックすると、ホストコントローラーの機能に関する詳細情報を取得できます。 リンクをクリックする代わりに、コマンドを入力することもできます。 たとえば、ホストコントローラーのリソース使用状況に関する情報を表示するには、コマンド **! xhci \_ resourceusage 0xfffffa800536e2d0**を入力します。

**メモ**   DML 機能は、WinDbg では使用できますが、Visual Studio または KD では使用できません。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

**! Xhci \_ dumpall**コマンドは、この一連のコマンドの親コマンドです。

-   [**! xhci \_ 機能**](-usb3kd-xhci-capability.md)
-   [**! xhci \_ info**](-usb3kd-xhci-info.md)
-   [**! xhci \_ デバイスのロット**](-usb3kd-xhci-deviceslots.md)
-   [**! xhci \_**](-usb3kd-xhci-commandring.md)
-   [**! xhci \_ eventring**](-usb3kd-xhci-eventring.md)
-   [**! 転送中の xhci \_**](-usb3kd-xhci-transferring.md)
-   [**! xhci \_ trb**](-usb3kd-xhci-trb.md)
-   [**! xhci \_ レジスタ**](-usb3kd-xhci-registers.md)
-   [**! xhci \_ resourceusage**](-usb3kd-xhci-resourceusage.md)

**! Xhci \_ dumpall**コマンドによって表示される情報は、USB 3.0 ホストコントローラードライバーによって管理されるデータ構造に基づいています。 Usb 3.0 ホストコントローラードライバーおよび USB 3.0 スタック内のその他のドライバーの詳細については、「 [Usb ドライバースタックアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。 USB 3.0 スタックのドライバーで使用されるデータ構造の詳細については、Windows 8 ビデオの[Usb デバッグイノベーション](https://channel9.msdn.com/Events/BUILD/BUILD2011/HW-258P)のパート2を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






