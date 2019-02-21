---
title: .createdir (セットの作成プロセスのディレクトリ)
description: .Createdir コマンドでは、デバッガーによって作成されたすべてのプロセスの開始ディレクトリとハンドルの継承を制御します。
ms.assetid: 797f5398-f0b4-48e9-bc5f-eac5a53cad67
keywords:
- .createdir (セットの作成プロセスのディレクトリ) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .createdir (Set Created Process Directory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a5245f42b272564849464fd2c57a794c9f73e43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530308"
---
# <a name="createdir-set-created-process-directory"></a>.createdir (セットの作成プロセスのディレクトリ)


**.Createdir**コマンドは、デバッガーによって作成されたすべてのプロセスの開始ディレクトリとハンドルの継承を制御します。

```dbgsyntax
.createdir [-i | -I] [Path] 
```

## <a name="span-idddkmetasetcreatedprocessdirectorydbgspanspan-idddkmetasetcreatedprocessdirectorydbgspanparameters"></a><span id="ddk_meta_set_created_process_directory_dbg"></span><span id="DDK_META_SET_CREATED_PROCESS_DIRECTORY_DBG"></span>パラメーター


<span id="_______-i______"></span><span id="_______-I______"></span> **-i**   
エラーの原因のプロセスがデバッガーからハンドルを継承するようにデバッガーによって作成されます。 これが既定値です。

<span id="_______-I______"></span><span id="_______-i______"></span> **-**   
デバッガーからハンドルを継承することから、デバッガーによって作成されたプロセスをできないようにします。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *パス*   
ターゲット プロセスのプロセスで作成されたすべての子プロセスの開始ディレクトリを指定します。 場合*パス*スペースが含まれることは、引用符で囲む必要があります。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

場合 **.createdir**使用は、パラメーターなしで、現在開始ディレクトリとハンドル継承状態が表示されます。

場合 **.createdir**がかつてない使用すると、作成プロセスは、通常の既定のディレクトリ ディレクトリとして使用の開始。 既にでパスを設定している場合 **.createdir**を使用して、既定の状態を返すと **.createdir""** 引用符で囲まれて何もします。

**.Createdir**設定によって作成されたすべてのプロセスに影響を与えます[ **(プロセスの作成) に関する**](-create--create-process-.md)します。 WinDbg のによって作成されたプロセスにも影響[ファイル |実行可能ファイルを開く](file---open-executable.md)メニュー コマンド、しない限り、**開始ディレクトリ**テキスト ボックスは、この設定を上書きに使用されます。

 

 





