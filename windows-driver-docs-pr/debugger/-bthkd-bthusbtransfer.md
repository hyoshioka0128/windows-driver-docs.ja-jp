---
title: bthkd.bthusbtransfer
description: Bthkd.bthusbtransfer コマンドには、バッファーの Irp、Bip および転送の情報を含む Bluetooth usb 転送コンテキストが表示されます。
ms.assetid: 61323238-E741-4291-A03C-F4060820D384
keywords:
- デバッグ bthkd.bthusbtransfer Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bthkd.bthusbtransfer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 149ea01dbed84299fd93fc5107737c8be31e07a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334661"
---
# <a name="bthkdbthusbtransfer"></a>!bthkd.bthusbtransfer


**! Bthkd.bthusbtransfer**コマンド Irp、Bip 転送バッファー情報を含む Bluetooth usb 転送コンテキストを表示します。

```dbgsyntax
!bthkd.bthusbtransfer addr 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______addr______"></span><span id="_______ADDR______"></span> *addr*   
Bluetooth USB 転送コンテキストのアドレス。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


使用することができます、! bthinfo コマンドは、USB 転送コンテキストのアドレスを表示します。 転送リスト セクションの下に表示されます。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Bthkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[Bluetooth の拡張機能 (Bthkd.dll)](bluetooh-extensions--bthkd-dll-.md)

 

 






