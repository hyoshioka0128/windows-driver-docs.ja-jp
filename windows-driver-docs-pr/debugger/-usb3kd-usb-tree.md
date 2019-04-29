---
title: usb3kd.usb_tree
description: Usb3kd.usb_tree 拡張機能では、すべての USB 3.0 コント ローラー、ハブ、およびコンピューター上のデバイスについてのツリー形式で情報が表示されます。
ms.assetid: 8E24AD44-7B32-4299-8428-D8E9B36F5848
keywords:
- デバッグ usb3kd.usb_tree Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.usb_tree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d6a8fef0d862caa8025ffb7b104746217264364b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330783"
---
# <a name="usb3kdusbtree"></a>! usb3kd.usb\_ツリー


[ **! Usb3kd.usb\_ツリー** ](-usb3kd-device-info.md)拡張機能では、すべての USB 3.0 コント ローラー、ハブ、およびコンピューター上のデバイスについてのツリー形式で情報が表示されます。

```dbgcmd
!usb3kd.usb_tree [1]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______1______"></span> **1**   
表示には、ハブおよびポートの状態情報が含まれています。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


次のスクリーン ショットの出力を示しています、 [ **! usb\_ツリー** ](-usb3kd-device-info.md)コマンド。

![出力、! usb\-コマンドが表示されたトポロジの列挙されたデバイスとハブのリストをツリー](images/usbtree01.png)

出力で始まる行で表される 1 つの USB 3.0 ホスト コントがあることを示しています。 [ **! xhci\_情報**](-usb3kd-xhci-info.md)します。 次の行では、ホスト コント ローラーのルート ハブを表します。 次の 4 つの行では、ルート ハブに関連付けられているポートを表します。 2 つのポートに接続されているデバイスがあることを確認できます。

出力を使用して[を使用してデバッガー マークアップ言語 (DML)](debugger-markup-language-commands.md)リンクを提供します。 リンクは、ツリー内の個々 のオブジェクトについての詳細情報を提供するコマンドを実行します。 たとえばのいずれかをクリックして接続されたデバイスのいずれかに関する情報を取得できます、 [ **! デバイス\_情報**](-usb3kd-device-info.md)リンク。 リンクをクリックする代わりに、コマンドを入力することができます。 たとえば、最初の接続されたデバイスに関する情報を表示することがコマンドを入力する **! デバイス\_情報 0xfffffa8004630690**します。

**注**  DML の機能は、WinDbg がではなく Visual Studio または KD で使用できます。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

[ **! Usb\_ツリー** ](-usb3kd-device-info.md)コマンドは、このコマンドのセットの親コマンド。

-   [**! ハブ\_情報**](-usb3kd-hub-info.md)
-   [**! ハブ\_情報\_から\_fdo**](-usb3kd-hub-info-from-fdo.md)
-   [**! デバイス\_情報**](-usb3kd-device-info.md)
-   [**! デバイス\_情報\_から\_pdo**](-usb3kd-device-info-from-pdo.md)
-   [**! ポート\_情報**](-usb3kd-port-info.md)

によって表示される情報、 [ **! usb\_ツリー** ](-usb3kd-device-info.md)コマンド ファミリは、USB 3.0 ハブ ドライバーによって維持されるデータ構造に基づきます。 USB 3.0 ハブのドライバーと USB 3.0 スタック内の他のドライバーについては、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)します。 USB 3.0 スタック内のドライバーで使用されるデータ構造の詳細については、第 2 部を参照してください、 [Windows 8 の USB デバッグ イノベーション](https://go.microsoft.com/fwlink/p/?LinkID=249153)ビデオ。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






