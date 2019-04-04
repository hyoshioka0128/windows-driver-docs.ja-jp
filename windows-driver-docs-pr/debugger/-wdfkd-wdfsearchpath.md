---
title: wdfkd.wdfsearchpath
description: Wdfkd.wdfsearchpath 拡張機能は、カーネル モード ドライバー フレームワーク (KMDF) エラー ログの記録用のファイルを書式設定する検索パスを設定します。
ms.assetid: cb52dc07-00b3-47d3-8636-4a6cd5ff3e29
keywords:
- デバッグ wdfkd.wdfsearchpath Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfsearchpath
api_location:
- Wdfkd.dll
api_type:
- DllExport
ms.localizationpriority: medium
ms.openlocfilehash: ccf2ce7ca4ac573a2fd419ef2ae9630f7226983b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572451"
---
# <a name="wdfkdwdfsearchpath"></a>!wdfkd.wdfsearchpath


**! Wdfkd.wdfsearchpath**拡張機能は、カーネル モード ドライバー フレームワーク (KMDF) エラー ログの記録用のファイルを書式設定する検索パスを設定します。

```dbgcmd
!wdfkd.wdfsearchpath Path
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *パス*   
KMDF の書式設定ファイルを格納するディレクトリのパス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク


KMDF 1、UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>コメント
-------

KMDF の書式設定ファイルは、Windows Driver Kit (WDK) で含まれています。 書式設定ファイルへのパスは、WDK のインストール ディレクトリとインストールされている、WDK のバージョンによって異なります。 KMDF の書式設定ファイルでは、拡張機能 tmf (トレース メッセージの書式設定) があります。 検索パスを決定するを参照または検索フォーム Wdf のファイル名の WDK インストール*VersionNumber*.tmf します。 次の例は、使用する方法を示します、 **! wdfkd.wdfsearchpath**拡張機能。

```dbgcmd
kd> !wdfsearchpath C:\WinDDK\7600\tools\tracing\amd64
```

トレース\_形式\_検索\_PATH 環境変数は、検索パスも制御しますが、 **! wdfkd.wdfsearchpath**拡張機能よりも優先される検索パスをトレース\_形式\_検索\_パスを指定します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">Wdfkd.dll</td>
</tr>
</tbody>
</table>

 

 





