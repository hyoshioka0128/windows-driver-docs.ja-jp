---
title: usb3kd.xhci_dumpall
description: Usb3kd.xhci_dumpall コマンドでは、コンピューターのすべての USB 3.0 ホスト コント ローラーに関する情報が表示されます。 表示は、UsbXhci.sys によって管理されるデータ構造に基づいています。
ms.assetid: D1087DC6-B065-48E3-93B2-EF53AE9DA8C7
keywords:
- デバッグ usb3kd.xhci_dumpall Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_dumpall
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7736dba8fbb19b3b0e73e7fe5a2cea85cfa7fae6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572486"
---
# <a name="usb3kdxhcidumpall"></a>! usb3kd.xhci\_dumpall


[ **! Usb3kd.xhci\_dumpall** ](-usb3kd-device-info.md)コマンドは、コンピューターのすべての USB 3.0 ホスト コント ローラーに関する情報を表示します。 表示は、USB 3.0 ホスト コント ローラー ドライバー (UsbXhci.sys) によって管理されるデータ構造に基づいています。

```dbgcmd
!usb3kd.xhci_dumpall [1]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_____________1"></span> **1**  
すべての XHCI コマンドを実行し、各コマンドの出力を表示します。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


次のスクリーン ショットの出力を表示する、 **! xhci\_dumpall**l コマンド。

![出力、! xhci\-dumpall コマンドが xhci コント ローラーの情報を表示](images/xhcidumpall01.png)

出力は、1 つの USB 3.0 ホスト コント ローラーがあることを示しています。

出力を使用して[を使用してデバッガー マークアップ言語 (DML)](debugger-markup-language-commands.md)リンクを提供します。 リンクは、USB 3.0 ホスト コント ローラーのドライバーによって維持されるように、ホスト コント ローラーの状態に関する詳細情報を提供するコマンドを実行します。 たとえば、すれば、ホストの詳細についてコント ローラーの機能をクリックして、 [ **! xhci\_機能**](-usb3kd-xhci-capability.md)リンク。 リンクをクリックする代わりに、コマンドを入力することができます。 たとえば、ホスト コント ローラーのリソース使用状況に関する情報を表示することがコマンドを入力する **! xhci\_resourceusage 0xfffffa800536e2d0**します。

**注**  DML の機能は、WinDbg がではなく Visual Studio または KD で使用できます。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>コメント
-------

**! Xhci\_dumpall**コマンドは、このコマンドのセットの親コマンド。

-   [**! xhci\_機能**](-usb3kd-xhci-capability.md)
-   [**! xhci\_情報**](-usb3kd-xhci-info.md)
-   [**!xhci\_deviceslots**](-usb3kd-xhci-deviceslots.md)
-   [**!xhci\_commandring**](-usb3kd-xhci-commandring.md)
-   [**!xhci\_eventring**](-usb3kd-xhci-eventring.md)
-   [**!xhci\_transferring**](-usb3kd-xhci-transferring.md)
-   [**! xhci\_trb**](-usb3kd-xhci-trb.md)
-   [**! xhci\_を登録します**](-usb3kd-xhci-registers.md)
-   [**! xhci\_resourceusage**](-usb3kd-xhci-resourceusage.md)

によって表示される情報、 **! xhci\_dumpall**コマンドのファミリは、USB 3.0 ホスト コント ローラー ドライバーによって管理されるデータ構造に基づいています。 USB 3.0 ホスト コント ローラーのドライバーと USB 3.0 スタック内の他のドライバーについては、[USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)を参照してください。 USB 3.0 スタック内のドライバーで使用されるデータ構造の詳細については、第 2 部を参照してください、 [Windows 8 の USB デバッグ イノベーション](https://go.microsoft.com/fwlink/p/?LinkID=249153)ビデオ。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






