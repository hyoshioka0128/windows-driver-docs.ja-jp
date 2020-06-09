---
title: usbkd. usbkd
description: Usbkd. usbkd コマンドは、指定された型の構造体のリンクリストを表示します。
ms.assetid: 503466EE-2246-4CE3-BCE7-6DC7D42DB86A
keywords:
- usbkd. usbkd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usblist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fbeedc82cadde926e61f1bd2bd47b2ad6f9f61bb
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533983"
---
# <a name="usbkdusblist"></a>!usbkd.usblist


**! Usbkd. usbkd**コマンドは、指定された型の構造体のリンクリストを表示します。

```dbgcmd
!usbkd.usblist ListAddr, ListType
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______ListAddr______"></span><span id="_______listaddr______"></span><span id="_______LISTADDR______"></span>*Listaddr*   
構造体のリンクリストのアドレス。 USB ポートドライバーによって管理されているリンクリストのアドレスを検索するには、 [**! usbhcdext**](-usbkd-usbhcdext.md)を使用します。 USB ハブドライバーによって管理されているリンクリストのアドレスを検索するには、 [**! usbhubext**](-usbkd-usbhubext.md)を使用します。

<span id="_______ListType______"></span><span id="_______listtype______"></span><span id="_______LISTTYPE______"></span>*Listtype*   
次のリストの種類のいずれかです。

| リストの種類 | 構造体                                |
|-----------|------------------------------------------|
| **BC**    | **usbport \_バス \_ コンテキスト**               |
| **EP**    | **usbport \_HCD \_ エンドポイント**              |
| **TT**    | **usbport \_トランザクション \_ 変換ツール**    |
| **DL**    | **usbport \_USBD \_ デバイス \_ ハンドル**       |
| **PL**    | **usbhub! \_デバイス \_ 拡張機能 \_ PDO**      |
| **シングル**    | **usbhub! \_ハブの \_ 例外 \_ レコード**      |
| **RL**    | **usbhub! \_ハブ \_ 参照 \_ リストの \_ エントリ** |
| **TL**    | **usbhub! \_ハブ \_ タイマー \_ オブジェクト**          |
| **WI-FI**    | **usbhub! \_ハブ作業 \_ 項目**               |
| **IO**    | **usbhub! \_IO \_ 一覧の \_ エントリ**             |
| **LA**    | **usbhub! \_ラッチ \_ リスト \_ エントリ**          |
| **CL**    | **usbhub! \_ポートの \_ 変更の \_ コンテキスト**       |
| **BL**    | **usbhub! \_SSP \_ ビジー \_ ハンドル**           |

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

リンクリストのアドレスを検索する方法の1つを次に示します。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 ...
   ...
```

上記の出力では、FDO のデバイス拡張機能のアドレスが、 [DML](debugger-markup-language-commands.md)コマンドの引数として表示されます **! ehci \_ info ffffe00001ca11a0**です。

DML コマンドをクリックするか、デバイス拡張機能のアドレスを[**! usbhcdext**](-usbkd-usbhcdext.md)に渡します。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001ca11a0

HC Flavor 1000  FDO ffffe00001ca1050
Root Hub: FDO ffffe00002320050 !hub2_info ffffe000023201a0
...
DeviceHandleList: !usblist ffffe00001ca23b8, DL
...
```

上記の出力では、ffffe00001ca23b8 は usbport のリンクリストのアドレスです **。 \_USBD \_ デバイス \_ ハンドル**構造体。

ここで、リンクリストのアドレスを **! usblist**に渡します。

```dbgcmd
0: kd> !usblist ffffe00001ca23b8, DL
list: ffffe00001ca23b8 DL
----------
!usbdevh ffffe000020f9590
SSP [IdleReady] (0)
PCI\VEN_Xxxx  Xxxx Corporation
Root Hub
DriverName :  
----------
!usbdevh ffffe00001bce250
SSP [IdleReady] (0)
USB\Xxxx  Xxxx Corporation
Speed: HIGH, Address:  1, PortPathDepth: 1, PortPath: [3 0 0 0 0 0]
DriverName :\Driver\USBSTOR      !devstack ffffe000053ef2a0
----------
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






