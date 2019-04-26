---
title: ah (アサーションの処理)
description: Ah コマンド コントロール、アサーションが特定のアドレスの状態を処理します。
ms.assetid: a55aa34f-c861-45de-bacf-92549ab98fdc
keywords:
- ah (アサーションの処理) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ah (Assertion Handling)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36ef3af780fb85093d8ad257543b8975c8e5800c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355018"
---
# <a name="ah-assertion-handling"></a>ah (アサーションの処理)


**Ah**コマンドは、特定のアドレスの状態を処理するアサーションを制御します。

```dbgcmd
ahb [Address] 
ahi [Address] 
ahd [Address] 
ahc 
ah 
```

## <a name="span-idddkcmdassertionhandlingdbgspanspan-idddkcmdassertionhandlingdbgspanparameters"></a><span id="ddk_cmd_assertion_handling_dbg"></span><span id="DDK_CMD_ASSERTION_HANDLING_DBG"></span>パラメーター


<span id="_______ahb______"></span><span id="_______AHB______"></span> **ahb**   
指定したアドレスにアサーションが失敗した場合、デバッガーを中断します。

<span id="_______ahi"></span><span id="_______AHI"></span> **ahi**  
指定したアドレスにアサーションの失敗は無視されます。

<span id="_______ahd______"></span><span id="_______AHD______"></span> **ahd**   
指定したアドレスには、何かアサーション処理情報を削除します。 この削除が原因と、デバッガーがそのアドレスの既定の状態に戻ります。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
アサーションの処理状態が設定されている命令のアドレスを指定します。 このパラメーターを省略した場合、デバッガーは、現在のプログラム カウンターを使用します。

<span id="_______ahc"></span><span id="_______AHC"></span> **ahc**  
現在のプロセスのすべてのアサーション処理情報を削除します。

<span id="_______ah______"></span><span id="_______AH______"></span> **ah**   
現在のアサーション処理の設定を表示します。

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
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

中断状態と状態、すべてのイベント コードの説明については、すべてのイベント、およびこの状態を制御するための他の方法の詳細の既定の状態の一覧を処理の詳細については、次を参照してください[を制御する例外とイベント](controlling-exceptions-and-events.md).

<a name="remarks"></a>注釈
-------

**Ah\\*** コマンドは、特定のアドレスの状態を処理するアサーションを制御します。 [ **Sx\* asrt** ](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)コマンドは、グローバルのアサーションの状態の処理を制御します。 使用する場合**ah\\*** デバッガー応答に基づいて、アドレスを特定し、assert が発生するため、 **ah\\*** 設定を無視し、 **sx\* asrt**設定します。

デバッガーには、アサーションが検出されると、最初に、デバッガーがその特定のアドレスの処理が構成されているかどうかをチェックします。 処理を構成していない場合、デバッガーには、グローバル設定が使用されます。

**Ah\\*** コマンドが現在のプロセスのみに影響します。 現在のプロセスの終了時にすべてのステータスの設定は失われます。

アサーションの処理状態の状態のみに影響を与えます\_アサーション\_例外の例外。 この処理は、カーネル モードの ASSERT ルーチンには影響しません。

 

 





