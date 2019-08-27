---
title: findfilelockowner
description: Findfilelockowner 拡張機能は、ブロックされているスレッドのすべてのスレッドを調べることによって、ファイルオブジェクトロックの所有者の検索を試みます。
ms.assetid: 0d6eabf4-e7ac-4536-beab-d3027720efa8
keywords:
- findfilelockowner Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- findfilelockowner
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2993e3e7147c9c60fe9300820e98e9c8ac5e9e5a
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025307"
---
# <a name="findfilelockowner"></a>!findfilelockowner


**! Findfilelockowner**拡張機能は、IopSynchronousServiceTail assert でブロックされていて、ファイルオブジェクトをパラメーターとして持つスレッドのすべてのスレッドを調べることによって、ファイルオブジェクトロックの所有者の検索を試みます。

```dbgcmd
!findfilelockowner [FileObject]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span>*FileObject*   
ファイルオブジェクトのアドレスを指定します。 *FileObject*を省略した場合、拡張機能は、 **IopAcquireFileObjectLock**でスタックしている現在のプロセス内のスレッドを検索し、スタックトレースからファイルオブジェクトアドレスを取得します。

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
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ファイルオブジェクトの詳細については、Microsoft Windows SDK のドキュメント、Windows Driver Kit (WDK) のドキュメント、および Mark Russinovich と David ソロモンによる*Microsoft windows の内部構造*に関するドキュメントを参照してください。

<a name="remarks"></a>コメント
-------

この拡張機能は、タイムアウトしたスレッドが**IopAcquireFileObjectLock**内のファイルを待機していた、クリティカルセクションのタイムアウトの後に最も役立ちます。 問題のあるスレッドが見つかると、この拡張機能は、要求に使用された IRP の復旧を試み、IRP を処理していたドライバーを表示しようとします。

拡張機能は、問題のあるスレッドが見つかるまでシステム内のすべてのスレッドのスタックを調べるため、完了するまでに時間がかかります。任意の時点\`で、ctrl キーを押しながら BREAK キー (WinDbg の場合) または ctrl + C (KD の場合) を押すことによって停止できます。

 

 





