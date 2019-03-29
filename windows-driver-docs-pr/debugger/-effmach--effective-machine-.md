---
title: .effmach (効果的なコンピューター)
description: .Effmach コマンドを表示またはデバッガーが使用するプロセッサ モードを変更します。
ms.assetid: bf4dfdc0-2f0b-416a-8bf2-0e7d81339905
keywords:
- 有効なマシン (.effmach) コマンド
- .effmach (効果的な Machine) Windows のデバッグ
ms.date: 01/24/2018
topic_type:
- apiref
api_name:
- .effmach (Effective Machine)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 65bf2b32e2b783f49eb841f9068a1a58ff48236b
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349829"
---
# <a name="effmach-effective-machine"></a>.effmach (効果的なコンピューター)


**.Effmach**コマンドを表示またはデバッガーが使用するプロセッサ モードを変更します。

```dbgcmd
.effmach [MachineType]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______MachineType______"></span><span id="_______machinetype______"></span><span id="_______MACHINETYPE______"></span> *MachineType*   
デバッガーがこのセッションで使用するプロセッサの種類を指定します。 このパラメーターを省略した場合、デバッガーには、現在のコンピューターの種類が表示されます。

次の種類のマシンのいずれかを入力できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>コンピューターの種類</strong></p></td>
<td align="left"><p><strong>[説明]</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>」を参照してください。</strong></p></td>
<td align="left"><p>対象のコンピュータのプロセッサのネイティブ モードのプロセッサ モードを使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>#</strong></p></td>
<td align="left"><p>最新のイベントのコードを実行しているプロセッサ モードを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>x86</strong></p></td>
<td align="left"><p>X86 ベースのプロセッサ モードを使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>amd64</strong></p></td>
<td align="left"><p>X64 ベース プロセッサ モードを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ebc</strong></p></td>
<td align="left"><p>EFI バイト コード プロセッサ モードを使用します。</p></td>
</tr>
</tr>
<tr class="odd">
<td align="left"><p><strong>arm</strong></p></td>
<td align="left"><p>ARM64 プロセッサ モードを使用します。</p></td>
</tr>
</tr>
<tr class="evenodd">
<td align="left"><p><strong>chpe</strong></p></td>
<td align="left"><p>CHPE プロセッサ モードを使用します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

プロセッサ モード デバッガーの多くの機能に影響を与えます。

-   プロセッサは、スタック トレースが使用されます。

-   かどうか、プロセスは、32 ビットまたは 64 ビットのポインターを使用します。

-   プロセッサの登録のセットがアクティブです。

 

 





