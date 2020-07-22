---
title: .echotimestamps (タイム スタンプの表示)
description: Echotimestamps コマンドは、タイムスタンプ情報の表示をオンまたはオフにします。
ms.assetid: c70dc71b-83c2-41de-90f3-638e231c0476
keywords:
- タイムスタンプの表示 (echotimestamps) コマンド
- タイムスタンプ
- DbgPrint タイムスタンプ
- . echotimestamps (タイムスタンプの表示) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .echotimestamps (Show Time Stamps)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0d76511842c15cb50b2a2757a23dcb5fc3f769f5
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873827"
---
# <a name="echotimestamps-show-time-stamps"></a>.echotimestamps (タイム スタンプの表示)


**Echotimestamps**コマンドは、タイムスタンプ情報の表示をオンまたはオフにします。

```dbgcmd
.echotimestamps 0 
.echotimestamps 1 
.echotimestamps 
```

## <a name="span-idddk_meta_show_time_stamps_dbgspanspan-idddk_meta_show_time_stamps_dbgspanparameters"></a><span id="ddk_meta_show_time_stamps_dbg"></span><span id="DDK_META_SHOW_TIME_STAMPS_DBG"></span>パラメータ


<span id="_______0______"></span>**0**   
タイムスタンプ情報の表示をオフにします。 これは、デバッガーの既定の動作です。

<span id="_______1______"></span> **1**   
タイムスタンプ情報の表示をオンにします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

**Dbgprint**、 **KdPrint**、 **Dbgprintex**、および**KdPrintEx**の詳細については、「[デバッグメッセージの読み取りとフィルター処理](reading-and-filtering-debugging-messages.md)」の「dbgprint Buffer」を参照してください。

<a name="remarks"></a>解説
-------

パラメーターを指定せずに**echotimestamps**コマンドを使用すると、タイムスタンプの表示がオンまたはオフになり、新しい状態が表示されます。

このディスプレイをオンにすると、デバッガーには、モジュールの読み込み、スレッドの作成、例外、およびその他のイベントのタイムスタンプが表示されます。

**Dbgprint**、 **KdPrint**、 **Dbgprintex**、および**KdPrintEx**のカーネルモードルーチンは、書式設定された文字列をホストコンピューター上のバッファーに送信します。 文字列は[デバッガーコマンドウィンドウ](debugger-command-window.md)に表示されます (このような印刷を無効にしている場合を除く)。 また、 [**! dbgprint**](-dbgprint.md) extension コマンドを使用して、書式設定された文字列を表示することもできます。

**Echotimestamps**を使用してタイムスタンプの表示をオンにすると、 **dbgprint**バッファー内の各コメントの日時が表示されます。

 

 





