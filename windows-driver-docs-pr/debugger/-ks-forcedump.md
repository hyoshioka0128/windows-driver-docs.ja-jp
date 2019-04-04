---
title: ks.forcedump
description: Ks.forcedump コマンドでは、呼び出し元が指定のアドレスでメモリの内容に関する情報が表示されます。
ms.assetid: 2829d324-a346-47af-a5f8-1808f329cadf
keywords:
- デバッグ ks.forcedump Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.forcedump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b423c675d4e5b9d5e50307eec9c0cafc5bc24c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549402"
---
# <a name="ksforcedump"></a>!ks.forcedump


**! Ks.forcedump**コマンドは、呼び出し元が指定のアドレスでメモリの内容に関する情報を表示します。

```dbgcmd
!ks.forcedump Object Type [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
情報を表示する対象のオブジェクトへのポインターを指定します。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *型*   
オブジェクトの種類を指定します。

AVStream/KS オブジェクト、*型*値は次のいずれかを指定する必要があります。CKsQueue、CKsDevice、CKsFilterFactory、CKsFilter、CKsPin、CKsRequestor、CKsSplitter、CKsSplitterBranch、CKsPipeSection、KSPIN、KSFILTER、KSFILTERFACTORY、KSDEVICE、KSSTREAM\_ポインター、KSPFRAME\_ヘッダー、KSIOBJECT\_ヘッダー、KSPDO\_拡張機能、KSIDEVICE\_ヘッダー、KSSTREAM\_ヘッダー、KSPIN\_記述子\_EX、CKsProxy、CKsInputPin、CKsOutputPin、CasyncItemHandler します。

ポート クラスのオブジェクトの*型*値は次のいずれかを指定する必要があります。デバイス\_コンテキスト、CPortWaveCyclic、CPortPinWaveCyclic、CPortTopology、CPortDMus、CIrpStream、CKsShellRequestor、CPortFilterWaveCyclic、CDmaChannel、CPortWavePci、CportPinWavePci します。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
(省略可能)。 0 ~ 7 で表示する詳細のレベルを指定の値を大きく表示徐々 に詳細なスケールします。 使用可能なすべての詳細を表示するには、7 の値を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

通常は、使用できる[ **! ks.dump** ](-ks-dump.md)データ構造を表示します。

ただし、シンボルが正しく読み込まれていないか、情報が多すぎるにページ型の識別ロジック アウトされた場合、 [ **! ks.dump** ](-ks-dump.md)コマンドが指定したアドレスに構造体の型を識別するために失敗します。

このような場合を使用して再試行してください、 **! ks.forcedump**コマンド。 このコマンドは機能と同じように[ **! ks.dump** ](-ks-dump.md)する点を除いて、ユーザーがオブジェクトの型を指定します。

**注**   、 **! ks.forcedump**コマンドがないことを確認します*型*で提供されるアドレスで構成の種類が正しく*オブジェクト*. これが、構造体の型であると見なします*オブジェクト*し、それに応じてデータを表示します。

 

発行することによってサポートされているすべてのオブジェクトの一覧を取得できる、 **! ks.forcedump**引数なしでコマンド。

出力の 2 つの例をここでは **! ks.forcedump**、用のフィルターのアドレスを使用して、*オブジェクト*引数が、さまざまなレベルの詳細。

```dbgcmd
kd> !forcedump 829493c4 KSFILTER
WARNING: I am dumping 829493c4 as a KSFILTER.
         No checking has been performed to ensure that it is this type!!!

Filter object 829493c4 [CKsFilter = 82949350]
    Descriptor     f7a233c8:
    Context        829dce28

kd> !forcedump 829493c4 KSFILTER 7
WARNING: I am dumping 829493c4 as a KSFILTER.
         No checking has been performed to ensure that it is this type!!!

Filter object 829493c4 [CKsFilter = 82949350]
    Descriptor     f7a233c8:
    Filter Category GUIDs:
        Video
        Capture
    Context        829dce28
    INTERNAL INFORMATION:
        Public Parent Factory   829782dc
        Aggregated Unknown      00000000
        Device Interface        823b83c8
        Control Mutex           829493f8 is not held
    Object Event List:
        None
    CKsFilter object 82949350 [KSFILTER = 829493c4]
        Processing Mutex         82949484 is not held
        Gate &                   82949464
        Gate.Count               1
        Pin Factories:
            Pin ID 0 [Video/General Capture Out]:
                Child Count        1
                Bound Child Count  1
                Necessary Count    0
                Specific Instances:
                    8293f580 
```

 

 





