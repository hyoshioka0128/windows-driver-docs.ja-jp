---
title: .srcnoisy (ノイズの多いソースの読み込み中)
description: .Srcnoisy コマンドでは、ソース ファイルの読み込みの詳細レベルを制御します。
ms.assetid: c57e0d0a-7903-455a-9a92-fab75f10ca80
keywords:
- .srcnoisy (ノイズの多いソースの読み込み中) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .srcnoisy (Noisy Source Loading)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aac70c4217d3cfef3f58b2b52aeabe4435d8f385
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559970"
---
# <a name="srcnoisy-noisy-source-loading"></a>.srcnoisy (ノイズの多いソースの読み込み中)


**.Srcnoisy**コマンドは、ソース ファイルの読み込みの詳細レベルを制御します。

```dbgcmd
.srcnoisy [Options]
```

## <a name="span-idddkmetanoisysourceloadingdbgspanspan-idddkmetanoisysourceloadingdbgspanparameters"></a><span id="ddk_meta_noisy_source_loading_dbg"></span><span id="DDK_META_NOISY_SOURCE_LOADING_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションのいずれかを指定できます。

<span id="0"></span>0  
余分なメッセージの表示を無効にします。

<span id="1"></span>1  
ソース ファイルの読み込みとアンロードの進行状況に関する情報が表示されます。

<span id="2"></span>2  
シンボル ファイルの読み込みとアンロードの進行状況に関する情報が表示されます。

<span id="3"></span>3  
オプション 1 と 2 に表示されるすべての情報が表示されます。

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

 

<a name="remarks"></a>注釈
-------

パラメーターなしで **.srcnoisy**ノイズの多いソースの読み込みの現在の状態が表示されます。

ノイズの多いソース読み込みする必要がありますと混同しない--によって制御されるノイズの多いシンボルの読み込み、 [ **! sym ノイズの多い**](-sym.md)拡張機能と他の方法を制御するので、 [SYMOPT\_デバッグ](symbol-options.md#symopt-debug)設定します。

 

 





