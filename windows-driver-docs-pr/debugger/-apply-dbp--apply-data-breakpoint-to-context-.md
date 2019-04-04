---
title: .apply_dbp (データ ブレークポイントをコンテキストに適用)
description: .Apply_dbp コマンドでは、指定されたレジスタのコンテキストに現在のプロセスの既存のデータ ブレークポイントが適用されます。
ms.assetid: c74fd4b3-3335-4e03-a57a-6a9aa883dd9f
keywords:
- .apply_dbp (コンテキストにデータ ブレークポイントを適用する) Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .apply_dbp (Apply Data Breakpoint to Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b86c00a0c785ae6f52172f918b076148eb1ef6d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551262"
---
# <a name="applydbp-apply-data-breakpoint-to-context"></a>.apply\_dbp (適用データ ブレークポイントのコンテキストに)


**.Apply\_dbp**コマンドでは、指定されたレジスタのコンテキストに現在のプロセスの既存のデータ ブレークポイントが適用されます。

```dbgcmd
    .apply_dbp [/m Context] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________m_______Context______"></span><span id="________m_______context______"></span><span id="________M_______CONTEXT______"></span> **/m** *コンテキスト*   
メモリを現在のプロセスのデータ ブレークポイントを適用するには、レジスタのコンテキスト (CONTEXT 構造) のアドレスを指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードとカーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ ターゲットのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

プロセッサによって制御されるブレークポイントの詳細については、[プロセッサ ブレークポイント (ba ブレークポイント)](processor-breakpoints---ba-breakpoints-.md)を参照してください。 レジスタのコンテキスト (スレッド コンテキスト) に関する詳細については、[登録コンテキスト](changing-contexts.md#register-context)を参照してください。

<a name="remarks"></a>注釈
-------

プロセッサによって制御されているブレークポイントが呼び出される*データ ブレークポイント*または*プロセッサ ブレークポイント*します。 これらのブレークポイントがによって作成された、 [ **ba (アクセスの切断)** ](ba--break-on-access-.md)コマンド。

これらのブレークポイントは、特定のプロセスのアドレス空間内のメモリ位置に関連付けられます。 **.Apply\_dbp**コマンドをこのコンテキストを使用するとこれらのデータ ブレークポイントがアクティブにできるように指定されたレジスタのコンテキストを変更します。

場合、 **/m** *アドレス*パラメーターが使用されないデータ ブレークポイントは、現在のレジスタのコンテキストに適用されます場合、。

このコマンドは、マシンのネイティブ モードで、ターゲットが場合にのみ使用できます。 たとえば、x86 をエミュレートする 64 ビット コンピューターで、ターゲットが実行されているプロセッサを使用して*WOW64*、このコマンドを使用することはできません。

このコマンドは、便利な時間の 1 つの例では、例外フィルターの場合です。 **.Apply\_dbp**コマンドは、例外フィルターの保存されているコンテキストを更新できます。 データ ブレークポイントは、例外フィルターを終了し、格納されたコンテキストが再開されるときに適用されます。 このような変更せずにデータ ブレークポイントは失われるなります。

 

 





