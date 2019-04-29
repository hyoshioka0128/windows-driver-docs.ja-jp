---
title: バグ チェック 0xCB の解釈
description: バグ チェック 0xCB の解釈
ms.assetid: 82951e2b-cbb2-45d2-a6b8-4fddece035ce
keywords:
- カーネル デバッグは、ストリーミング ビデオ ストリームの停止のバグ チェック 0xcb
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eed9d18e7fe58a525f8f48af33990c6a23f30b28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327337"
---
# <a name="interpreting-bug-check-0xcb"></a>バグ チェック 0xCB の解釈


ビデオ ストリーム stall のデバッグに関連付けられている最も一般的なバグ チェック コードはバグ チェック 0xCB (ドライバー\_左\_ロック\_ページ\_IN\_プロセス)。 そのパラメーターの詳細な一覧を参照してください。 [**バグ チェック 0xCB**](bug-check-0xcb--driver-left-locked-pages-in-process.md)します。

バグ チェックが発生したときに表示されるメッセージは、原因として、Ks.sys をポイントします。

```dbgcmd
Use !analyze -v to get detailed debugging information.
BugCheck CB, {f90c6ae0, f9949215, 81861788, 26}
Probably caused by : ks.sys ( ks!KsProbeStreamIrp+333 )
```

として、推奨される使用[ **。-v を分析**](-analyze.md)より詳細な情報を取得します。

```dbgcmd
kd> !analyze -v
DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS (cb)
Caused by a driver not cleaning up completely after an I/O.
When possible, the guilty driver's name (Unicode string) is printed on
the bugcheck screen and saved in KiBugCheckDriver.
Arguments:
Arg3: 81861788, A pointer to the MDL containing the locked pages.
```

これで、使用、 [ **! 検索**](-search.md) MDL ポインターに関連付けられている仮想アドレスを検索する拡張機能。

```dbgcmd
kd> !search 81861788
Searching PFNs in range 00000001 - 0000FF76 for [FFFFFFFF81861788 - FFFFFFFF81861788]

Pfn      Offset   Hit      Va       Pte
- - - - - - - - - - - - - - - - - - - - - - - - - - -
000008A7 00000B0C 81861788 808A7B0C C020229C
00000A04 00000224 16000001 80A04224 C0202810
...
00001732 000009B4 81861788 817329B4 C0205CC8
```

各仮想アドレス (VA) が見つかりません、IRP の署名を探します。 使用して、 [ **dd** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンド 1 つの DWORD マイナス VA を実行します。

```dbgcmd
kd> dd 808A7B0C-4 l4
808a7b08  f9949215 81861788 00000026 00000000
kd> $ Not an Irp
kd> dd 80A04224-4 l4
80a04220  00000000 00000000 00000000 00000000
kd> $ Not an Irp
kd> dd 817329B4-4 l4
817329b0  01900006 81861788 00000070 ffa59220
kd> $ Matches signature
```

IRP シグネチャを持つ、VA が見つかると後で使用して、 [ **! irp** ](-irp.md)が保留中でどのようなドライバーを検索する拡張機能でこの IRP。

```dbgcmd
kd> !irp 817329b0 7
Irp is active with 2 stacks 2 is current (= 0x81732a44)
 Mdl = 81861788 System buffer = ffa59220 Thread 00000000:  Irp stack trace.
>[  e, 0]   1  1 81a883c8 81ae6158 00000000-00000000    pending
 \Driver\TESTCAP
                        Args: 00000070 00000000 002f4017 00000000
```

この場合、\\ドライバー\\TESTCAP バグ チェックの可能性が高い原因であります。

 

 





