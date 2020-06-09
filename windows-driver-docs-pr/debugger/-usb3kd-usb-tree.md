---
title: usb_tree usb3kd
description: Usb3kd 拡張機能には、コンピューター上のすべての USB 3.0 コントローラー、ハブ、およびデバイスに関する情報がツリー形式で表示されます usb_tree。
ms.assetid: 8E24AD44-7B32-4299-8428-D8E9B36F5848
keywords:
- usb3kd Windows デバッグの usb_tree
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.usb_tree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 29e8ab20e02d07e821cde2d22653f1936b5a0dd3
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534899"
---
# <a name="usb3kdusb_tree"></a>! usb3kd \_ ツリー


[**! Usb3kd \_ ツリー**](-usb3kd-device-info.md)拡張には、コンピューター上のすべての usb 3.0 コントローラー、ハブ、およびデバイスに関する情報がツリー形式で表示されます。

```dbgcmd
!usb3kd.usb_tree [1]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______1______"></span>**1**   
表示には、ハブとポートの状態情報が含まれます。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


次のスクリーンショットは、 [**! usb \_ ツリー**](-usb3kd-device-info.md)コマンドの出力を示しています。

![\-トポロジで列挙されたデバイスとハブリストを示す! usb ツリーコマンドの出力](images/usbtree01.png)

出力には、USB 3.0 ホストコントローラーが1つあることが示されています。これは、 [**! xhci \_ info**](-usb3kd-xhci-info.md)で始まる行で表されます。 次の行は、ホストコントローラーのルートハブを表します。 次の4つの行は、ルートハブに関連付けられているポートを表します。 2つのポートにデバイスが接続されていることを確認できます。

出力では、[デバッガーマークアップ言語 (DML) を使用して](debugger-markup-language-commands.md)リンクを提供します。 リンクは、ツリー内の個々のオブジェクトに関する詳細情報を提供するコマンドを実行します。 たとえば、いずれかの[**デバイス \_ 情報**](-usb3kd-device-info.md)リンクをクリックすると、接続されているデバイスの1つに関する情報を取得できます。 リンクをクリックする代わりに、コマンドを入力することもできます。 たとえば、最初に接続されたデバイスに関する情報を表示するには、コマンド「**デバイス \_ 情報 0xfffffa8004630690**」を入力します。

**メモ**   DML 機能は、WinDbg では使用できますが、Visual Studio または KD では使用できません。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

[**! Usb \_ ツリー**](-usb3kd-device-info.md)コマンドは、この一連のコマンドの親コマンドです。

-   [**! ハブ \_ 情報**](-usb3kd-hub-info.md)
-   [**! \_ \_ fdo からのハブ情報 \_**](-usb3kd-hub-info-from-fdo.md)
-   [**! デバイス \_ 情報**](-usb3kd-device-info.md)
-   [**! \_ \_ pdo からのデバイス情報 \_**](-usb3kd-device-info-from-pdo.md)
-   [**! ポート \_ 情報**](-usb3kd-port-info.md)

[**! Usb \_ ツリー**](-usb3kd-device-info.md)ファミリのコマンドによって表示される情報は、usb 3.0 hub ドライバーによって管理されるデータ構造に基づいています。 Usb 3.0 hub ドライバーおよび USB 3.0 スタックのその他のドライバーの詳細については、「 [Usb ドライバースタックアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。 USB 3.0 スタックのドライバーで使用されるデータ構造の詳細については、Windows 8 ビデオの[Usb デバッグイノベーション](https://channel9.msdn.com/Events/BUILD/BUILD2011/HW-258P)のパート2を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






