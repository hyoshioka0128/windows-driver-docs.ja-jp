---
title: findfilelockowner
description: Findfilelockowner 拡張機能がブロックされているスレッドのすべてのスレッドを調べることで、ファイル オブジェクトのロックの所有者を検索しようとするとします。
ms.assetid: 0d6eabf4-e7ac-4536-beab-d3027720efa8
keywords:
- Windows デバッグ findfilelockowner
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- findfilelockowner
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 331d20203285de5a75eda12d785b5e767c7b9ff2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337118"
---
# <a name="findfilelockowner"></a>!findfilelockowner


**! Findfilelockowner**拡張機能を持つファイル オブジェクトをパラメーターとして IopSynchronousServiceTail アサートでブロックされたスレッドのすべてのスレッドを調べることで、ファイル オブジェクトのロックの所有者を検索しようとしました。

```dbgcmd
!findfilelockowner [FileObject]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span> *FileObject*   
ファイル オブジェクトのアドレスを指定します。 場合*FileObject*を省略すると、任意のスレッドでスタックしている現在のプロセスで、拡張機能を検索**IopAcquireFileObjectLock**およびスタック トレースからのファイル オブジェクトのアドレスを取得します。

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

ファイル オブジェクトについては、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

内のファイルを待機していたスレッドがタイムアウトするクリティカル セクション タイムアウト後にこの拡張機能は最も役に立つ**IopAcquireFileObjectLock**します。 問題のあるスレッドが見つかると、要求に使用された IRP を回復して、IRP を処理しているドライバーを表示する、拡張機能と試行されます。

拡張機能では、問題のあるスレッドが見つかるまで、システムですべてのスレッドのスタックを走査、ために、完了に時間がかかります。停止する\`(WinDbg) では、CTRL + BREAK または (KD) では、CTRL + C を押して任意の時点。

 

 





