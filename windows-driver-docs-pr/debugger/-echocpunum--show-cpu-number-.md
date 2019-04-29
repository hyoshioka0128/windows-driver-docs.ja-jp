---
title: .echocpunum (CPU 番号の表示)
description: .Echocpunum コマンドは、オンまたはマルチプロセッサの対象のコンピュータをデバッグするときに、プロセッサ番号の表示をオフにします。
ms.assetid: a238b291-8c6e-4a4c-adc3-3be5a9916a29
keywords:
- CPU の数 (.echocpunum) コマンドを表示します。
- マルチプロセッサ コンピューターで、CPU の数を表示する (.echocpunum) コマンド
- .echocpunum (CPU 数を表示する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .echocpunum (Show CPU Number)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fead002bd508311910785e453d4e3ab067cd2c62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336798"
---
# <a name="echocpunum-show-cpu-number"></a>.echocpunum (CPU 番号の表示)


**.Echocpunum**コマンドが有効にまたはマルチプロセッサの対象のコンピュータをデバッグするときに、プロセッサ番号の表示をオフにします。

```dbgcmd
.echocpunum 0 
.echocpunum 1 
.echocpunum 
```

## <a name="span-idddkmetashowcpunumberdbgspanspan-idddkmetashowcpunumberdbgspanparameters"></a><span id="ddk_meta_show_cpu_number_dbg"></span><span id="DDK_META_SHOW_CPU_NUMBER_DBG"></span>パラメーター


<span id="_______0______"></span> **0**   
プロセッサ番号の表示をオフにします。

<span id="_______1______"></span> **1**   
プロセッサ番号の表示をオンにします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

マルチプロセッサ コンピューターをデバッグする方法の詳細については、次を参照してください。[マルチプロセッサ構文](multiprocessor-syntax.md)します。

<a name="remarks"></a>注釈
-------

使用する場合、 **.echocpunum**引数を含まないコマンド プロセッサ番号の表示がオンまたはオフになっているし、新しい状態が表示されます。

既定では、表示はになります。

 

 





