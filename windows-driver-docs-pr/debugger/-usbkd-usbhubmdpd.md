---
title: usbhubmdpd
description: Usbhubmdpd コマンドは、バグチェック0xFE の結果として生成されたクラッシュダンプに存在する場合、usbhub _HUB_PORT_DATA 構造体を表示します。
ms.assetid: 128D45A2-A891-42BC-9E3E-FCDC5B4504A2
keywords:
- usbhubmdpd Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubmdpd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 648d96225bf334b9a709a8e45083c00dd63c539d
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534693"
---
# <a name="usbkdusbhubmdpd"></a>!usbkd.usbhubmdpd


**Usbhubmdpd**コマンドを実行すると、 **usbhub \_ が表示されます。\_ \_ ** [**バグチェック 0xfe**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプに存在するハブポートデータ構造。

```dbgcmd
!usbkd.usbhubmdpd [PortNum]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______PortNum______"></span><span id="_______portnum______"></span><span id="_______PORTNUM______"></span>*Portnum*   
USB ポート番号。 ポート番号を指定した場合、このコマンドは、指定されたポートを表す構造体 (存在する場合) を表示します。 ポート番号を指定しない場合、このコマンドは、[**バグチェック 0xfe**](bug-check-0xfe--bugcode-usb-driver.md)が開始された構造 (存在する場合) を表示します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="remarks"></a>注釈
-------

このコマンドは、[**バグチェック 0xfe: バグコード \_ USB \_ ドライバー**](bug-check-0xfe--bugcode-usb-driver.md)の結果として生成されたクラッシュダンプファイルをデバッグする場合にのみ使用します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






