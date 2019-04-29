---
title: wdfkd.wdfumdownirp
description: Wdfkd.wdfumdownirp 拡張機能では、指定されたユーザー モードの IRP に関連付けられているカーネル モード I/O 要求パケット (IRP) が表示されます。
ms.assetid: 98DFF193-950A-46CF-875E-B2907743F5D4
keywords:
- デバッグ wdfkd.wdfumdownirp Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumdownirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fee9988cb58e9e49f833d7f727286478823fc977
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323157"
---
# <a name="wdfkdwdfumdownirp"></a>!wdfkd.wdfumdownirp


**! Wdfkd.wdfumdownirp**拡張機能には、指定されたユーザー モードの IRP に関連付けられているカーネル モード I/O 要求パケット (IRP) が表示されます。 このコマンドは、2 つの手順で使用されます。 注釈をご覧ください。

```dbgcmd
!wdfkd.wdfumdownirp UmIrp [FileObject] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______UmIrp______"></span><span id="_______umirp______"></span><span id="_______UMIRP______"></span> *UmIrp*   
ユーザー モード IRP のアドレスを指定します。 使用することができます[ **! wdfkd.wdfumirps** ](-wdfkd-wdfumirps.md)で UM Irp のアドレスを取得、[暗黙的なプロセス](controlling-threads-and-processes.md)します。

<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span> *FileObject*   
アドレスを指定します、 **\_ファイル\_オブジェクト**構造体。 このアドレスを取得する方法については、「解説」を参照してください。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

または UMDF ホスト プロセス (wudfhost.exe) に関連付けられているユーザー モードのデバッグ セッションでカーネル モードのデバッグ セッションでは、このコマンドを使用することができます。

このコマンドを使用するには、次の手順に従います。

1.  ユーザー モード IRP アドレスのみを渡して、このコマンドを入力します。 コマンドには、ハンドルが表示されます。
2.  表示されるハンドルを渡す、 [ **! 処理**](-handle.md)コマンド。 出力に **! 処理**のアドレスを見つけ、 **\_ファイル\_オブジェクト**構造体。
3.  このコマンドを入力、もう一度両方のユーザー モードの IRP のアドレスとのアドレスを渡す、 **\_ファイル\_オブジェクト**構造体。

 

 





