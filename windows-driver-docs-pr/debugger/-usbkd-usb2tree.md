---
title: usb2tree
description: Usb2tree コマンドは、USB 2.0 ツリーを表示します。
ms.assetid: 6BEFE154-C8F0-466C-AB68-71C6304D0DEA
keywords:
- usb2tree Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usb2tree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c965428d3db1d3db617515903fba3bf90a8553b1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534869"
---
# <a name="usbkdusb2tree"></a>!usbkd.usb2tree


**Usb2tree**コマンドは、 [USB 2.0 ツリー](usb-2-0-extensions.md#usb-2-tree)を表示します。

```dbgcmd
!usbkd.usb2tree
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


このスクリーンショットは、 **! usb2tree**コマンドの出力の例を示しています。

![uhci ehci 情報と列挙されたハブリストを示す、! usb2tree コマンドの出力](images/usb2tree01.png)

出力には、1つの EHCI 実行単位と2つの UHCI 実行単位が示されています。 この例で示されている実行単位は、1つの USB ホストコントローラーデバイス上に存在します。 出力には、ルートハブと接続されているデバイスも表示されます。

出力では、[デバッガーマークアップ言語 (DML) を使用して](debugger-markup-language-commands.md)リンクを提供します。 リンクは、ツリー内のオブジェクトに関連する詳細情報を提供するコマンドを実行します。 たとえば、 [**! devobj**](-devobj.md)リンクの1つをクリックすると、EHCI 実行単位に関連付けられている機能デバイスオブジェクトに関する情報を取得できます。 リンクをクリックする代わりに、コマンドを手動で入力することもできます。 **! devobj ffffe00001ca7050**

**メモ**   DML 機能は、WinDbg では使用できますが、Visual Studio または KD では使用できません。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

**! Usb2tree**コマンドは、多くの[USB 2.0 デバッガー拡張コマンド](usb-2-0-extensions.md)の親コマンドです。 これらのコマンドによって表示される情報は、次のドライバーによって管理されるデータ構造に基づいています。

-   usbehci (USB 2 ホストコントローラー用ミニポートドライバー)
-   usbuhci (USB 2 ホストコントローラー用ミニポートドライバー)
-   usbport (USB 2 ホストコントローラー用ポートドライバー)
-   usbhub (USB 2 ハブドライバー)

これらのドライバーの詳細については、「 [Windows の USB ホスト側ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






