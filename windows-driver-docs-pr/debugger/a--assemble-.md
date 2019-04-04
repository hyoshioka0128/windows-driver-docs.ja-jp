---
title: (アセンブリ)
description: コマンドがアセンブル 32 ビット x86 命令ニーモニックおよび結果として得られる命令がメモリにコードを配置します。
ms.assetid: 6736a5fd-5a33-4698-9510-8a95f6a1caf7
keywords:
- (A) コマンドをアセンブルします。
- アセンブリのアセンブリ (a) コマンドをデバッグします。
- (アセンブリ) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- a (Assemble)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f77510936fbc6d3073b300b1ccd52a4cf5c531e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556485"
---
# <a name="a-assemble"></a>(アセンブリ)


**、** コマンド アセンブル 32 ビット x86 命令ニーモニックおよび結果として得られる命令がメモリにコードを配置します。

```dbgcmd
a [Address]
```

## <a name="span-idddkcmdassembledbgspanparameters"></a><span id="DDK_CMD_ASSEMBLE_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
結果として得られるコードを配置する場所のメモリ ブロックの先頭を指定します。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

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

アセンブリの詳細については、デバッグ、および関連するコマンドを参照してください[モードのアセンブリでのデバッグ](debugging-in-assembly-mode.md)します。

<a name="remarks"></a>注釈
-------

**、** コマンドは、64 ビット命令ニーモニックをサポートしていません。 ただし、 **、** 対象が 32 ビットまたは 64 ビット ターゲットのどちらをデバッグしているかどうかに関係なくコマンドが有効にします。 X86 および x64 の命令の間の類似点が原因も使用できます、 **、** 64 ビット ターゲットのデバッグ時に正常にコマンドします。

アドレスを指定しない場合、アセンブリ命令ポインターの現在の値を指定するアドレスから始まります。 新しい命令をアセンブルし、目的のニーモニックを入力し、ENTER キーを押します。 アセンブリを終了するには、のみ ENTER キーを押します。

アセンブラーは、すべてのコードで参照される記号を検索するため、このコマンドには完了までに時間がかかる場合があります。 この期間中、することはできませんキーを押して[ **CTRL + C**](ctrl-c--break-.md)を終了する、 **、** コマンド。

 

 





