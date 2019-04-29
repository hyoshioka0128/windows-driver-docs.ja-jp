---
title: usbkd.usblist
description: Usbkd.usblist コマンドでは、指定した型の構造体のリンク リストを表示します。
ms.assetid: 503466EE-2246-4CE3-BCE7-6DC7D42DB86A
keywords:
- デバッグ usbkd.usblist Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usblist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5fc12ab035d9d562879de195baf6225bf74ee212
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323597"
---
# <a name="usbkdusblist"></a>!usbkd.usblist


**! Usbkd.usblist**コマンドは、指定した型の構造体のリンク リストを表示します。

```dbgcmd
!usbkd.usblist ListAddr, ListType
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______ListAddr______"></span><span id="_______listaddr______"></span><span id="_______LISTADDR______"></span> *ListAddr*   
構造体のリンク リストのアドレス。 USB ポート ドライバーによって管理されるリンクのリストのアドレスを確認する[ **! usbhcdext**](-usbkd-usbhcdext.md)します。 USB ハブのドライバーによって管理されるリンクされたリストのアドレスを確認する[ **! usbhubext**](-usbkd-usbhubext.md)します。

<span id="_______ListType______"></span><span id="_______listtype______"></span><span id="_______LISTTYPE______"></span> *ListType*   
次のリスト型の 1 つ。

| リストの種類 | 構造体                                |
|-----------|------------------------------------------|
| **ビジネス継続性**    | **usbport!\_BUS\_コンテキスト**               |
| **EP**    | **usbport!\_HCD\_エンドポイント**              |
| **TT**    | **usbport!\_トランザクション\_トランスレーター**    |
| **DL**    | **usbport!\_USBD\_デバイス\_処理**       |
| **PL**    | **usbhub!\_デバイス\_拡張子\_PDO**      |
| **EL**    | **usbhub!\_ハブ\_例外\_レコード**      |
| **RL**    | **usbhub!\_ハブ\_参照\_一覧\_エントリ** |
| **TL**    | **usbhub!\_ハブ\_タイマー\_オブジェクト**          |
| **WI**    | **usbhub!\_ハブ\_作業項目**               |
| **IO**    | **usbhub!\_IO\_一覧\_エントリ**             |
| **LA**    | **usbhub!\_ラッチ\_一覧\_エントリ**          |
| **CL**    | **usbhub!\_ポート\_変更\_コンテキスト**       |
| **BL**    | **usbhub!\_SSP\_ビジー\_処理**           |

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>例
--------

リンク リストのアドレスを検索する 1 つの方法を次に示します。 最初に入力[ **! usbkd.usb2tree**](-usbkd-usb2tree.md)します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 ...
   ...
```

上記の出力の引数として、FDO のデバイスの拡張機能のアドレスを表示、 [DML](debugger-markup-language-commands.md)コマンド **! ehci\_情報 ffffe00001ca11a0**します。

DML コマンドをクリックするか、デバイスの拡張機能のアドレスを渡す[ **! usbhcdext**](https://msdn.microsoft.com/library/windows/hardware/dn367072)します。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001ca11a0

HC Flavor 1000  FDO ffffe00001ca1050
Root Hub: FDO ffffe00002320050 !hub2_info ffffe000023201a0
...
DeviceHandleList: !usblist ffffe00001ca23b8, DL
...
```

上記の出力のリンク リストのアドレスになります ffffe00001ca23b8**し、usbport!\_USBD\_デバイス\_処理**構造体。

リンクされたリストのアドレスを渡すようになりました **! usblist**します。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






