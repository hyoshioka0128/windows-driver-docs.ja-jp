---
title: CTRL + A (トグル ボー レート)
description: Ctrl キーを押しながら A キーは、カーネル デバッグ接続で使用するボー レートを切り替えます。
ms.assetid: 77a95ca1-073c-480a-abda-f484adbc1d23
keywords:
- CTRL + A (トグル ボー レート) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+A (Toggle Baud Rate)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d31a1e41d2efe29af5f2feb2f73ad88605250b9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559554"
---
# <a name="ctrla-toggle-baud-rate"></a>CTRL + A (トグル ボー レート)


Ctrl キーを押しながら A キーは、カーネル デバッグ接続で使用するボー レートを切り替えます。

KD 構文

```dbgcmd
CTRL+A  ENTER 
```

WinDbg の構文

```dbgcmd
CTRL+ALT+A 
```

## <span id="ddk_meta_ctrl_a_dbg"></span><span id="DDK_META_CTRL_A_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>デバッガー</strong></p></td>
<td align="left"><p>KD と WinDbg のみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

これは、カーネル デバッグ接続をすべて使用可能なボー レートを循環します。

サポートされているボー レートは 38400、19200、57600、および 115200 です。 このコントロールのキーが使用されるたびに、[次へ] のボー レートが選択されます。 ボー レートが既に 115200 にいる場合は、19200 差し引かれます。

WinDbg では、このことができますもすることで実現選択[デバッグ |カーネルの接続 |ボー レートをサイクル](debug---kernel-connection---cycle-baud-rate.md)します。

実際には、ボー レートをデバッグする位置を変更するこのコントロールのキーを使うことはできません。 ホスト コンピューターと対象コンピューターのボー レートが一致する必要がありを再起動しなくても、ターゲット コンピューターのボー レートを変更することはできません。 そのため、のみ、2 台のコンピューターは、異なるレートで通信するために試行している場合は、ボー レートを切り替える必要があります。 この場合、ターゲット コンピューターの一致するように、ホスト コンピューターのボー レートを変更する必要があります。

 

 





