---
title: Ctrl + D (デバッグ情報の切り替え)
description: CTRL + D キーは、オンとオフをデバッガー内部情報のフローを切り替えます。 これは、デバッガーが正しく通信できていない場合、通信を再開に使用されます。
ms.assetid: fcc5d597-6a3f-4d6c-82f9-3624efb4f434
keywords:
- CTRL + D (デバッグ情報の表示/非表示) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+D (Toggle Debug Info)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3907900b3bdc971293c9aae752738d2c6445952d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374964"
---
# <a name="ctrld-toggle-debug-info"></a>Ctrl + D (デバッグ情報の切り替え)


CTRL + D キーは、オンとオフをデバッガー内部情報のフローを切り替えます。 これは、デバッガーが正しく通信できていない場合、ターゲット コンピューターとホスト コンピューター間の通信を再開に使用されます。

KD 構文

```dbgcmd
CTRL+D  ENTER 
```

WinDbg の構文

```dbgcmd
CTRL+ALT+D 
```

## <span id="ddk_meta_ctrl_d_dbg"></span><span id="DDK_META_CTRL_D_DBG"></span>


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

これをオンにすると、デバッガーは、ホスト コンピューターと対象のコンピュータ間の通信に関する情報を出力します。

このキーは、デバッガーがクラッシュしたかどうかをテストに使用できます。 デバッガーまたはターゲットのいずれかが固定されることが疑われる場合は、このキーを使用します。 送信されるパケットを表示する場合、ターゲットは引き続き取り組んでいます。 タイムアウト メッセージが表示された場合、ターゲットが応答しません。 ない場合のメッセージに、デバッガーがクラッシュしました。

ターゲットが応答していない場合は、CTRL + R ENTER CTRL + C を使用します。 タイムアウト メッセージがまだ表示される場合、ターゲットがクラッシュした (または、デバッガーが正しく構成されていません)。

またこれは、KD デバッガー自体のデバッグに役立ちます。

 

 





