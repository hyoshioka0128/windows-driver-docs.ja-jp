---
title: .noversion (バージョン チェックを無効にする)
description: .Noversion コマンドには、すべてのバージョンの拡張 Dll のチェックが無効にします。
ms.assetid: ce7fbff4-7936-4bef-8236-a13957ada7f4
keywords:
- バージョン チェック (.noversion) コマンドを無効にします。
- .noversion (バージョン チェックを無効にする) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .noversion (Disable Version Checking)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a1c329dba7aa9953fb4210fd32996dd42bc62146
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335865"
---
# <a name="noversion-disable-version-checking"></a>.noversion (バージョン チェックを無効にする)


**.Noversion**コマンドは、すべてのバージョンの拡張 Dll のチェックを無効にします。

```dbgcmd
.noversion
```

## <span id="ddk_meta_disable_version_checking_dbg"></span><span id="DDK_META_DISABLE_VERSION_CHECKING_DBG"></span>


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

 

<a name="remarks"></a>注釈
-------

拡張 Dll のビルド番号は、コンピューター、Dll がコンパイルされ、特定のバージョンのデータ構造体への依存関係にリンクされているため、デバッグ中のビルド番号と一致する必要があります。 バージョンが一致しない場合通常、次のメッセージを受信します。

```console
*** Extension DLL(1367 Free) does not match target system(1552 Free) 
```

 

 





