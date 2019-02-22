---
title: .unload (拡張 DLL のアンロード)
description: .Unload コマンドでは、デバッガーから拡張 DLL をアンロードします。
ms.assetid: 8399e4a8-0265-4690-b35f-973b69fe2764
keywords:
- 拡張 DLL (.unload) コマンドをアンロードします。
- 拡張機能のコマンド (コマンド)、拡張 DLL のアンロード (.unload) コマンド
- .unload (拡張 DLL のアンロード) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .unload (Unload Extension DLL)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b25de3865a9d6d04e066fba1eb64f50e15c20ab6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558235"
---
# <a name="unload-unload-extension-dll"></a>.unload (拡張 DLL のアンロード)


**.Unload**コマンドは、デバッガーから拡張 DLL をアンロードします。

```dbgcmd
.unload DLLName 
!DLLName.unload
```

## <a name="span-idddkmetaunloadextensiondlldbgspanspan-idddkmetaunloadextensiondlldbgspanparameters"></a><span id="ddk_meta_unload_extension_dll_dbg"></span><span id="DDK_META_UNLOAD_EXTENSION_DLL_DBG"></span>パラメーター


<span id="_______DLLName______"></span><span id="_______dllname______"></span><span id="_______DLLNAME______"></span> *DLLName*   
デバッガー拡張を読み込む DLL のファイル名を指定します。 DLL が読み込まれるときに、完全なパスが指定されている場合で指定する完全なここでも、必要があります。 場合*DLLName*は省略すると、現在の拡張 DLL をアンロードします。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、読み込み、アンロード、および拡張機能を制御するを参照してください[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)します。

<a name="remarks"></a>注釈
-------

このコマンドは、作成する拡張機能をテストする場合に便利です。 拡張機能を再コンパイルするは、アンロードし、し、新しい DLL を読み込む必要があります。

 

 





