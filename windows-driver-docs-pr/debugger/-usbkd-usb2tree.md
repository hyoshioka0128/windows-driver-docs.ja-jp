---
title: usbkd.usb2tree
description: Usbkd.usb2tree コマンドには、USB 2.0 のツリーが表示されます。
ms.assetid: 6BEFE154-C8F0-466C-AB68-71C6304D0DEA
keywords:
- デバッグ usbkd.usb2tree Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usb2tree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a47edbfe78880ed2ea784bf79c55e6ff9f1fb49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581744"
---
# <a name="usbkdusb2tree"></a>!usbkd.usb2tree


**! Usbkd.usb2tree**コマンドが表示されます[USB 2.0 ツリー](usb-2-0-extensions.md#usb-2-tree)します。

```dbgcmd
!usbkd.usb2tree
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


このスクリーン ショットの表示と出力の例、 **! usb2tree**コマンド。

![出力、! uhci ehci 情報と、ハブの列挙リストを示す usbkd.usb2tree コマンド](images/usb2tree01.png)

出力は、EHCI の実行の 1 つの単位と UHCI 実行の 2 つの単位を示します。 この例に示すように実行単位は、1 つの USB ホスト コント ローラー デバイス上にある発生します。 出力は、ルート ハブと接続されているデバイスにも表示されます。

出力を使用して[を使用してデバッガー マークアップ言語 (DML)](debugger-markup-language-commands.md)リンクを提供します。 リンクは、ツリー内のオブジェクトに関連する詳細な情報を提供するコマンドを実行します。 いずれかをクリックするなど、 [ **! devobj** ](-devobj.md) EHCI 実行ユニットに関連付けられているリンク機能のデバイス オブジェクトに関する情報を取得します。 リンクをクリックする代わりに、でしたのコマンドは、手動で入力する: **! devobj ffffe00001ca7050**

**注**  DML の機能は、WinDbg がではなく Visual Studio または KD で使用できます。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>コメント
-------

**! Usb2tree**コマンドは、多くの親コマンド、 [USB 2.0 デバッガー拡張機能コマンド。](usb-2-0-extensions.md) これらのコマンドで表示される情報は、これらのドライバーによって管理されるデータ構造に基づいています。

-   usbehci.sys (2 の USB ホスト コント ローラーのミニポート ドライバー)
-   usbuhci.sys (2 の USB ホスト コント ローラーのミニポート ドライバー)
-   usbport.sys (2 の USB ホスト コント ローラーのポート ドライバー)
-   usbhub.sys (USB 2 hub ドライバー)

これらのドライバーの詳細については、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p/?LinkId=251983)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






