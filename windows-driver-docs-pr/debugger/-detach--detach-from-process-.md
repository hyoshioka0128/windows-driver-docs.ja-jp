---
title: .detach (プロセスからデタッチ)
description: .Detach コマンドでは、デバッグ セッションを終了が、実行されているすべてのユーザー モード ターゲット アプリケーションのままです。
ms.assetid: 4f0fbd8b-3037-4549-99da-be40a091a363
keywords:
- .detach (プロセスからデタッチ) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .detach (Detach from Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b16176b96fe6cc3acda159c547c2120555b42fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549431"
---
# <a name="detach-detach-from-process"></a>.detach (プロセスからデタッチ)


**.Detach**コマンドは、デバッグ セッションは終わりますが、ユーザー モードのターゲット アプリケーションの実行中のままです。

```dbgcmd
.detach [ /h | /n ]
```

## <a name="span-idddkmetadetachfromprocessdbgspanspan-idddkmetadetachfromprocessdbgspanparameters"></a><span id="ddk_meta_detach_from_process_dbg"></span><span id="DDK_META_DETACH_FROM_PROCESS_DBG"></span>パラメーター


<span id="________h______"></span><span id="________H______"></span> **/h**   
未処理のデバッグ イベントは続きし、処理済みとしてマークします。 これが既定値です。

<span id="________n______"></span><span id="________N______"></span> **/n**   
処理済みとしてマークしなくても、未処理のデバッグ イベントが引き続き行われます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

ライブ ユーザー モード デバッグは、このコマンドは、Windows XP および Windows の以降のバージョンでのみサポートします。

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

このコマンドは、デバッグ セッションで、次のシナリオのいずれかになります。

-   ユーザー モードまたはカーネル モードのダンプ ファイルをデバッグする際にします。

-   ライブ ユーザー モードのターゲットをデバッグする際にします。

-   ときに、ユーザー モード ターゲット noninvasively デバッグ。

ターゲットは 1 つのみをデバッグする場合、デバッガーは、デタッチ後に休止モードに返します。

場合[複数のターゲットをデバッグ](debugging-multiple-targets.md)、デバッグ セッションは残りのターゲットに進みます。

 

 





