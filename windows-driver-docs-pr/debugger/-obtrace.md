---
title: obtrace
description: Obtrace 拡張機能は、指定したオブジェクトのオブジェクト参照のトレース データを表示します。
ms.assetid: 6a124f9f-1c2f-4303-b84f-0032fb912cc1
keywords:
- Windows デバッグ obtrace
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- obtrace
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 28eb455d377c3ce9e0442528aa2291f9240b1d0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334473"
---
# <a name="obtrace"></a>!obtrace


**! Obtrace**拡張機能は、指定したオブジェクトのオブジェクト参照のトレース データを表示します。

```dbgcmd
!obtrace Object
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
オブジェクトまたはパスへのポインター。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

グローバル フラグ ユーティリティ (GFlags) の詳細については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

Windows のオブジェクト参照のトレース機能は、オブジェクトの参照カウンターはインクリメントまたはデクリメントされるたびに、シーケンシャルなスタック トレースを記録します。

オブジェクト参照のトレース データを表示するこの拡張機能を使用する前に使用する必要があります[GFlags](gflags.md)有効にする[オブジェクト参照トレース](object-reference-tracing.md)指定したオブジェクト。 カーネル フラグ (実行時) の設定として、変更がすぐには有効がシャット ダウンまたは再起動する場合は表示されなくなりますのオブジェクト参照のトレースを有効にすることができます。またはレジストリ設定としてが、再起動が必要ですが、変更するまで有効なままになります。

出力の例を次に示します、 **! obtrace**拡張機能。

```dbgcmd
kd> !obtrace 0xfa96f700
Object: fa96f700        Image: cmd.exe
Sequence  (+/-)  Stack
--------  -----  ---------------------------------------------------
   2421d    +1  nt!ObCreateObject+180
                nt!NtCreateEvent+92
                nt!KiFastCallEntry+104
                nt!ZwCreateEvent+11
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   2421e    -1  nt!ObfDereferenceObject+19
                nt!NtCreateEvent+d4
                nt!KiFastCallEntry+104
                nt!ZwCreateEvent+11
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   2421f    +1  nt!ObReferenceObjectByHandle+1c3
                win32k!xxxCreateThreadInfo+37d
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   24220    +1  nt!ObReferenceObjectByHandle+1c3
                win32k!ProtectHandle+22
                win32k!xxxCreateThreadInfo+3a0
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   24221    -1  nt!ObfDereferenceObject+19
                win32k!xxxCreateThreadInfo+3a0
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

----  ----------------------------------------------------------
References: 3, Dereferences 2
```

内のプライマリ インジケーター、 **! obtrace 0xfa96f700**表示は次の表に記載します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>シーケンス</strong></p></td>
<td align="left"><p>操作の順序を表します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>+/-</strong></p></td>
<td align="left"><p>参照または逆参照操作を示します。</p>
<p>+1 では、参照操作を示します。</p>
<p>-1 は、逆参照操作を示します。</p>
<p>n +/-複数の参照/逆参照操作を示します。</p></td>
</tr>
</tbody>
</table>

 

X64 ベースのターゲット コンピューター上のオブジェクト参照トレース不完全になるため、常にパッシブより大きい IRQL レベルでのスタック トレースを取得することはできません\_レベル。

CTRL + BREAK (WinDbg) で、または (KD) では、CTRL + C を押して、いつでも実行を停止できます。

 

 





