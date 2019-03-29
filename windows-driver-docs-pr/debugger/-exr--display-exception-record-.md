---
title: .exr (例外レコードの表示)
description: .Exr コマンドには、例外レコードの内容が表示されます。
ms.assetid: 786d7ee0-45d7-489c-b53b-28349ea10e36
keywords:
- 例外レコード (.exr) コマンドが表示されます。
- 例外レコード
- .exr (例外レコードの表示) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .exr (Display Exception Record)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3acae875f16df0a2d1c2517bc31d1c005c73119e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574279"
---
# <a name="exr-display-exception-record"></a>.exr (例外レコードの表示)


**.Exr**コマンド例外レコードの内容を表示します。

```dbgcmd
.exr Address 
.exr -1
```

## <a name="span-idddkmetadisplayexceptionrecorddbgspanspan-idddkmetadisplayexceptionrecorddbgspanparameters"></a><span id="ddk_meta_display_exception_record_dbg"></span><span id="DDK_META_DISPLAY_EXCEPTION_RECORD_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
例外レコードのアドレスを指定します。 指定した場合 **-1**アドレスとして、デバッガーは、最新の例外が表示されます。

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

**.Exr**コマンドには、ターゲット コンピューターで、デバッガーが発生した例外に関連する情報が表示されます。 表示される情報には、例外のアドレス、例外コード、例外フラグ、および例外にパラメーターの変数の一覧が含まれています。

通常取得することができます、*アドレス*を使用して、 [ **! pcr** ](-pcr.md)拡張機能。

**.Exr** 0x1E のバグ チェックをデバッグする多くの場合、コマンドを使用します。 詳細と例では、次を参照してください。 [**バグ チェック 0x1E** ](bug-check-0x1e--kmode-exception-not-handled.md) (KMODE\_例外\_いない\_処理済み)。

 

 





