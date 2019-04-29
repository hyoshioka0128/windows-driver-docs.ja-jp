---
title: minipkd.adapters
description: Minipkd.adapters 拡張機能では、すべてのシステムでは、識別された SCSI ポート ドライバーと連動するアダプターが表示され、個々 のデバイスは、各アダプターに関連付けられています。
ms.assetid: 8571b9ec-1ec9-4adb-8a65-5306e45c3aa6
keywords:
- デバッグ minipkd.adapters Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.adapters
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b87b3883bf345ce8b394b75fa7ba7d5cb26724e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336093"
---
# <a name="minipkdadapters"></a>!minipkd.adapters


**! Minipkd.adapters**拡張機能では、すべてのシステムでは、識別された SCSI ポート ドライバーと連動するアダプターが表示されます、個々 のデバイスは、各アダプターに関連付けられているとします。

```dbgcmd
!minipkd.adapters 
```

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
<td align="left"><p>Minipkd.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。 [SCSI ミニポート デバッグ](scsi-miniport-debugging.md)します。

<a name="remarks"></a>注釈
-------

表示には、ドライバー名、デバイス オブジェクトのアドレス、および各アダプターのデバイスの拡張機能のアドレスが含まれています。 各アダプターの表示には、アダプターでは、各デバイスの一覧も含まれています。 各デバイスの表示には、デバイスの拡張機能のアドレス、SCSI アドレス、デバイス オブジェクトのアドレス、およびデバイスの一部のフラグが含まれます。 プラグ アンド プレイの状態や電源の状態に関する情報も含まれています。

次の表では、表示のフラグがについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>c</p></td>
<td align="left"><p>要求しています。 デバイスに、上のドライバーがあることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>m</p></td>
<td align="left"><p>不足しています。 デバイスが前回のスキャンにバス上に存在していたが、最新のスキャン中に存在しませんでしたを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>列挙されます。 プラグ アンド プレイのマネージャーにデバイスが報告されていることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>v</p></td>
<td align="left"><p>表示されます。 システムによって、デバイスが列挙されていることを示します。 デバイスに存在しない場合、このフラグはより重要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>p</p></td>
<td align="left"><p>ページングします。 ページングのパスで、デバイスがあることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>d</p></td>
<td align="left"><p>ダンプします。 デバイスがクラッシュ ダンプのパスでは、クラッシュ ダンプに使用されることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>h</p></td>
<td align="left"><p>休止状態にします。 デバイスが休止状態にならないことを示します。</p></td>
</tr>
</tbody>
</table>

 

次の例に示します、 **! minipkd.adapters**表示。

```dbgcmd
0: kd> !minipkd.adapters
Adapter \Driver\lp6nds35     DO 86334a70         DevExt 86334b28
Adapter \Driver\adpu160m     DO 8633da70         DevExt 8633db28
 LUN 862e60f8 @(0,0,0) c ev     pnp(00/ff) pow(0,0) DevObj 862e6040
 LUN 863530f8 @(0,1,0) c ev p d pnp(00/ff) pow(0,0) DevObj 86353040
 LUN 862e50f8 @(0,2,0) c ev     pnp(00/ff) pow(0,0) DevObj 862e5040
 LUN 863520f8 @(0,6,0)   ev     pnp(00/ff) pow(0,0) DevObj 86352040
Adapter \Driver\adpu160m     DO 86376040         DevExt 863760f8
```

次のようなエラー メッセージは、シンボル パスに誤りがあり、Scsiport.sys 記号の正しいバージョンを指していないか、SCSI ポート ドライバーと連携するすべてのアダプターを識別する Windows されていないことを示します。

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

場合、 [ **! minipkd.help** ](-minipkd-help.md)返しますヘルプ情報を正常に SCSI ポート シンボルでは、適切な拡張機能コマンド。

 

 





