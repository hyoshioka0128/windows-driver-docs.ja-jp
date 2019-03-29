---
title: irpfind
description: Irpfind 拡張機能では、ターゲット システムで、または指定した検索条件に一致するこれらの Irp に現在割り当てられているすべての I/O 要求パケット (IRP) に関する情報が表示されます。
ms.assetid: f0d850d9-8804-40df-90a3-b9c6a6b4540f
keywords:
- Windows デバッグ irpfind
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- irpfind
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fede13a247b35ebc4ec556b41a461c1eac7354d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575036"
---
# <a name="irpfind"></a>!irpfind


**! Irpfind**拡張機能またはその Irp が指定した検索条件に一致するすべての I/O 要求パケット (IRP) が、ターゲット システムに現在割り当てられているに関する情報を表示します。

構文

```dbgcmd
!irpfind [-v][PoolType[RestartAddress[CriteriaData]]]
```

## <a name="span-idddkirpfinddbgspanspan-idddkirpfinddbgspanparameters"></a><span id="ddk__irpfind_dbg"></span><span id="DDK__IRPFIND_DBG"></span>パラメーター


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
詳細な情報を表示します。

<span id="_______PoolType______"></span><span id="_______pooltype______"></span><span id="_______POOLTYPE______"></span> *PoolType*   
検索対象のプールの種類を指定します。 次の値が許可されています。

<span id="0"></span>0  
非ページ メモリ プールを指定します。 既定値です。

<span id="1"></span>1  
ページ メモリ プールを指定します。

<span id="2"></span>2  
特別なプールを指定します。

<span id="4"></span>4  
セッションのプールを指定します。

<span id="_______RestartAddress______"></span><span id="_______restartaddress______"></span><span id="_______RESTARTADDRESS______"></span> *RestartAddress*   
検索を開始する位置の 16 進数のアドレスを指定します。 これは、前回の検索が途中で終了した場合に役立ちます。 既定値は 0 です。

<span id="_______Criteria______"></span><span id="_______criteria______"></span><span id="_______CRITERIA______"></span> *条件*   
検索の条件を指定します。 のみそれら Irp を満たす特定の一致が表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条件</th>
<th align="left">一致</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>arg</strong></p></td>
<td align="left"><p>引数のいずれかと等しい場合、スタックの場所ですべての Irp を検索します<em>データ</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>デバイス</strong></p></td>
<td align="left"><p>スタックの場所ですべての Irp の検索場所<strong>デバイス オブジェクト</strong>と等しい<em>データ</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>fileobject</strong></p></td>
<td align="left"><p>すべての Irp を検索しますが<strong>Irp.Tail.Overlay.OriginalFileObject</strong> equals<em>データ</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>mdlprocess</strong></p></td>
<td align="left"><p>すべての Irp を検索しますが<strong>Irp.MdlAddress.Process</strong> equals<em>データ</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>thread</strong></p></td>
<td align="left"><p>すべての Irp を検索しますが<strong>Irp.Tail.Overlay.Thread</strong> equals<em>データ</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>userevent</strong></p></td>
<td align="left"><p>すべての Irp を検索しますが<strong>Irp.UserEvent</strong> equals<em>データ</em>。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span> *データ*   
検索に一致するデータを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドのアプリケーション。 Irp の詳細については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。

<a name="remarks"></a>コメント
-------

この例では、非ページ プールのユーザー イベント FF9E4F48 完了時に設定することで、IRP を検索します。

```dbgcmd
kd> !irpfind 0 0 userevent ff9e4f48
```

次の例では、すべての非ページ プール内のすべての Irp の一覧が生成されます。

```dbgcmd
kd> !irpfind
Searching NonPaged pool (8090c000 : 8131e000) for Tag: Irp
8097c008 Thread 8094d900 current stack belongs to  \Driver\symc810
8097dec8 Thread 8094dda0 current stack belongs to  \FileSystem\Ntfs
809861a8 Thread 8094dda0 current stack belongs to  \Driver\symc810
809864e8 Thread 80951ba0 current stack belongs to  \Driver\Mouclass
80986608 Thread 80951ba0 current stack belongs to  \Driver\Kbdclass
80986728 Thread 8094dda0 current stack belongs to  \Driver\symc810
```

 

 





