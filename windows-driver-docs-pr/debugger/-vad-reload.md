---
title: vad_reload
description: Vad_reload 拡張機能は、そのプロセスの仮想アドレス記述子 (Vad) を使用して、指定されたプロセスのユーザー モードのモジュールを再読み込みします。
ms.assetid: B5500227-DDC5-43aa-987B-EB02C59B3AC6
keywords:
- Windows デバッグ vad_reload
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vad_reload
api_location:
- Kdextx86.dll
- Kdexts.dll
api_type:
- DllExport
ms.localizationpriority: medium
ms.openlocfilehash: a613455ad75bd32ac60561ae7f4005fc8b45df18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325940"
---
# <a name="vadreload"></a>! vad\_を再読み込み


**! Vad\_を再読み込み**拡張機能は、そのプロセスの仮想アドレス記述子 (Vad) を使用して指定されたプロセスのユーザー モードのモジュールを再読み込みします。

```dbgcmd
!vad_reload Process
```

## <a name="span-idddkvaddbgspanspan-idddkvaddbgspanparameters"></a><span id="ddk__vad_dbg"></span><span id="DDK__VAD_DBG"></span>パラメーター


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *プロセス*   
モジュールが読み込まれるプロセスの 16 進数のアドレスを指定します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Vad については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

使用することができます、 [ **! プロセス**](-process.md)プロセスのアドレスを検索する拡張機能。

住所を検索しで使用する方法の例を次に示します、 **! vad\_を再読み込み**コマンド。

```dbgcmd
3: kd> !process 0 0
. . .
PROCESS fffffa8007d54450
    SessionId: 1  Cid: 115c    Peb: 7ffffef6000  ParentCid: 0c58
    DirBase: 111bc3000  ObjectTable: fffff8a006ae0960  HandleCount: 229.
    Image: SearchProtocolHost.exe
. . .
3: kd> !vad_reload fffffa8007d54450
fffffa80`04f5e8b0: VAD maps 00000000`6c230000 - 00000000`6c26bfff, file cscobj.dll
fffffa80`04e8f890: VAD maps 00000000`6ef90000 - 00000000`6f04afff, file mssvp.dll
fffffa80`07cbb010: VAD maps 00000000`6f910000 - 00000000`6faf5fff, file tquery.dll
fffffa80`08c1f2a0: VAD maps 00000000`6fb80000 - 00000000`6fb9bfff, file mssprxy.dll
fffffa80`07dce8b0: VAD maps 00000000`6fba0000 - 00000000`6fba7fff, file msshooks.dll
fffffa80`04fd2e70: VAD maps 00000000`72a50000 - 00000000`72a6cfff, file userenv.dll
. . .
```

<a name="requirements"></a>要件
------------

**DLL**

Kdexts.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**! プロセス**](-process.md)

[**! vad**](-vad.md)

 

 






