---
title: wudfext.umirp
description: Wudfext.umirp 拡張機能では、ホストのユーザー モード I/O 要求パケット (IRP UM) に関する情報が表示されます。
ms.assetid: b31b864d-0c94-48b8-9ffd-f14639b9a551
keywords:
- デバッグ wudfext.umirp Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 62439be90140eecbfc96604b7bd8f91e22cac56e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573107"
---
# <a name="wudfextumirp"></a>!wudfext.umirp


**! Wudfext.umirp**拡張機能は、ホストのユーザー モード I/O 要求パケット (IRP UM) に関する情報を表示します。

```dbgcmd
!wudfext.umirp Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
に関する情報を表示するには、UM IRP のアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>コメント
-------

使用することができます、 [ **! wudfext.umirps** ](-wudfext-umirps.md)ホスト プロセスですべて未処理 UM Irp の一覧を表示する拡張機能コマンド。

各 UM IRP では、スタックの 1 つまたは複数の場所があります。 各スタックの場所は、要求を処理するために呼び出された場合、デバイス スタックの 1 つのドライバーが受け取るパラメーターに対応します。

**! wudfext.umirp**ダンプのすべてのスタックの場所と右の山かっこによって現在の位置をマーク (&gt;)。 現在の場所は、要求を現在所有しているドライバーに対応します。 現在の場所、ドライバーは、[次へ] の下ドライバー スタックでは、またはドライバーがドライバーを所有する要求を完了すると、要求を転送するときに変更します。

例を次に、 **! wudfext.umirp**表示。

```dbgcmd
kd> !umirp 3dd480 
UM IRP: 0x003dd480  UniqueId: 0xde  Kernel Irp: 0x0x85377850
  Type: WudfMsg_READ
  ClientProcessId: 0x338
  Device Stack: 0x0034e4e0
  IoStatus
    hrStatus: 0x0
    Information: 0x0
  Driver/Framework created IRP: No
  Data Buffer: 0x00000000 / 0
  IsFrom32BitProcess: Yes
  CancelFlagSet: No
  Cancel callback: 0x01102224
  Total number of stack locations: 2
  CurrentStackLocation: 2 (StackLocation[ 1 ])
    StackLocation[ 0 ]
      UNINITIALIZED
  > StackLocation[ 1 ]
      IWDFRequest:  ????
      IWDFDevice:   0x000f2f80
      IWDFFile:     0x003a7648
      Completion:
        Callback:   0x00000000
        Context:    0x00000000
      Parameters: (RequestType: WdfRequestRead)
        Buffer length:        0x400
        Key:                  0x00000000
        Offset:               0x0
```

 

 





