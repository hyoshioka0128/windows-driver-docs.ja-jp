---
title: .lines (ソース行サポートの切り替え)
description: .Lines コマンドでは、有効またはソース行情報のサポートを無効にします。
ms.assetid: 5d923592-7aba-42a0-893b-2c6621e4b87f
keywords:
- .lines (切り替えのソース行のサポート) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .lines (Toggle Source Line Support)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ffb6803028bbe2e28dca3c015ca302a8c3770f5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571693"
---
# <a name="lines-toggle-source-line-support"></a>.lines (ソース行サポートの切り替え)


**.Lines**コマンドを有効またはソース行情報のサポートを無効にします。

```dbgcmd
.lines [-e|-d|-t]
```

## <a name="span-idddkmetatogglesourcelinesupportdbgspanspan-idddkmetatogglesourcelinesupportdbgspanparameters"></a><span id="ddk_meta_toggle_source_line_support_dbg"></span><span id="DDK_META_TOGGLE_SOURCE_LINE_SUPPORT_DBG"></span>パラメーター


<span id="_______-e______"></span><span id="_______-E______"></span> **-e**   
ソースの行のサポートを有効します。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
ソースの行のサポートを無効にします。

<span id="_______-t______"></span><span id="_______-T______"></span> **-t**   
ソースのライン サポートのオンまたはオフになります。 パラメーターを指定しない場合 **.lines**の既定の動作、 **.lines**コマンドは、この切り替えのソース行をサポートします。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ソースのデバッグと関連するコマンドの詳細については、次を参照してください。[元のモードでデバッグ](debugging-in-source-mode.md)します。

<a name="remarks"></a>コメント
-------

ソース レベルのデバッグを実行する前に、ソース行のサポートを有効にする必要があります。 このサポートにより、ソース行のシンボルを読み込むデバッガーです。

使用してソース行のサポートを有効にすることができます、 **.lines**コマンドまたは[-コマンド ライン オプションを行](command-line-options.md)します。 ソース行のサポートはまだ有効に、使用する場合、 **.lines**コマンドは、このサポートを無効にします。

使用しない場合、既定で、 **.lines**コマンド、WinDbg をオンにソース行のサポート、およびコンソール デバッガー (KD、CDB、NTSD) が、サポートを無効にします。 この設定を変更する方法の詳細については、次を参照してください。[シンボル オプションを設定](symbol-options.md)します。

 

 





