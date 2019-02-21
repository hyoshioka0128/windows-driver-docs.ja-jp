---
title: usbkd.usbhubmdpd
description: Usbkd.usbhubmdpd コマンドでは、0 xfe のバグ チェックの結果として生成されたクラッシュ ダンプに存在する場合、usbhub _HUB_PORT_DATA 構造が表示されます。
ms.assetid: 128D45A2-A891-42BC-9E3E-FCDC5B4504A2
keywords:
- デバッグ usbkd.usbhubmdpd Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubmdpd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5a849afa27ddd2e644f3d0fbe62f1ece3594f563
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558588"
---
# <a name="usbkdusbhubmdpd"></a>!usbkd.usbhubmdpd


**! Usbkd.usbhubmdpd**コマンドが表示されます、 **usbhub!\_ハブ\_ポート\_データ**の結果として生成されたクラッシュ ダンプに存在する場合に構造体[**バグ チェック 0 xfe**](bug-check-0xfe--bugcode-usb-driver.md)します。

```dbgcmd
!usbkd.usbhubmdpd [PortNum]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______PortNum______"></span><span id="_______portnum______"></span><span id="_______PORTNUM______"></span> *PortNum*   
USB ポートの番号。 (いずれかが存在する) 場合に、このコマンドが、構造体を表示しますポート番号を指定する場合、指定したポートを表します。 このコマンドを (1 つが存在する) 場合、構造を表示するポート番号を指定しない場合[**バグ チェック 0 xfe** ](bug-check-0xfe--bugcode-usb-driver.md)が開始されました。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>注釈
-------

結果として生成されたクラッシュ ダンプ ファイルをデバッグしている場合にのみ、このコマンドを使用して[ **0 xfe のバグ チェック。BUGCODE\_USB\_ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






