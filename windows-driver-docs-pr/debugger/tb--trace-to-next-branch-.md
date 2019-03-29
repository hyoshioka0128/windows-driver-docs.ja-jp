---
title: tb (次のブランチまでトレース)
description: Tb コマンドは、分岐命令に到達するまでプログラムを実行します。
ms.assetid: 28b736f9-69f5-405b-9684-48b4205e7633
keywords:
- tb (トレースを次の分岐に) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tb (Trace to Next Branch)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c32e3f437b69aa4d04a0dfdfa4e2fce141d5a3e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570767"
---
# <a name="tb-trace-to-next-branch"></a>tb (次のブランチまでトレース)


**Tb**コマンドは、分岐命令に到達するまでにプログラムを実行します。

```dbgcmd
tb [r] [= StartAddress] [Count] 
```

## <a name="span-idddkcmdtracetonextbranchdbgspanspan-idddkcmdtracetonextbranchdbgspanparameters"></a><span id="ddk_cmd_trace_to_next_branch_dbg"></span><span id="DDK_CMD_TRACE_TO_NEXT_BRANCH_DBG"></span>パラメーター


<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、 **tbr**、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_- reg コマンドを許可します。 これらすべてのコマンドの同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 4 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 使用しない場合*StartAddress*命令を命令ポインターが指すから実行が開始します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
許可する分岐の数を指定します。 分岐が検出されるたびに、命令アドレスおよび命令が表示されます。 省略した場合*カウント*既定値は 1 です。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p></p>
<strong>x86 ベースします。</strong>カーネル モードのみ<strong>Itanium ベースします。</strong>ユーザー モードでは、カーネル モード<strong>x64 ベースします。</strong>ユーザー モードでは、カーネル モード</td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>x86 ベース (GenuineIntel プロセッサ ファミリ 6 およびそれ以降)、itanium、x64 ベース</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドの詳細については、次を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>コメント
-------

**Tb**コマンドが実行を開始するようにターゲットを実行します。 この実行では、ブランチ コマンドに到達するまで続行されます。

作成する任意のブランチ コマンドで実行が停止します。 この停止中の実行が常にに基づいて、*逆アセンブル*コード、デバッガーがソース モードの場合にもします。

ジャンプ、カウントは、ループ、および while ループ、分岐命令を返します。 呼び出しが含まれます。 デバッガーには、無条件分岐、または条件が true の条件付き分岐が発生すると、実行を停止します。 かどうか、デバッガーは条件が false の条件分岐を検出すると、実行が続行されます。

実行が停止したら、分岐命令と関連付けられているシンボルのアドレスが表示されます。 この情報は、矢印とし、アドレスと手順については、新しいプログラム カウンターの場所の続きます。

**Tb**コマンドは、現在のプロセッサでのみ使用できます。 使用する場合**tb**ブランチ コマンドに達したとき、または別のプロセッサのイベントが発生した、どちらか早いマルチプロセッサ システムで実行を停止します。

通常は、プロセッサ制御ブロック (PRCB) が初期化された後は、ブランチのトレースが有効にします。 (、PRCB はブート プロセスの早い段階で初期化されます)。ただし、使用する必要がある場合、 **tb**この時点で、前にコマンドを使用することができます[ **.force\_tb (強制的に許可するブランチ トレース)** ](-force-tb--forcibly-allow-branch-tracing-.md)ブランチのトレースを有効にするには先ほどの。 使用して、 **.force\_tb**プロセッサの状態を破損することがあるため、慎重に行ってコマンドします。

 

 





