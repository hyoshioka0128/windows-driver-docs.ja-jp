---
title: wmitrace.searchpath
description: Wmitrace.searchpath 拡張機能では、トレース バッファー内のメッセージのトレース メッセージのフォーマット ファイルの場所を指定します。
ms.assetid: 528c997c-007c-4046-92cc-169c7720b3fe
keywords:
- デバッグ wmitrace.searchpath Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.searchpath
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0c55996754f97b744b3bc6595c0ce3a3c8caf301
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347238"
---
# <a name="wmitracesearchpath"></a>!wmitrace.searchpath


**! Wmitrace.searchpath**拡張機能は、トレース バッファー内のメッセージのトレース メッセージのフォーマット ファイルの場所を指定します。

```dbgcmd
!wmitrace.searchpath [+] TMFPath 
!wmitrace.searchpath
```

## <a name="span-idddkwmitracesearchpathdbgspanspan-idddkwmitracesearchpathdbgspanparameters"></a><span id="ddk__wmitrace_searchpath_dbg"></span><span id="DDK__WMITRACE_SEARCHPATH_DBG"></span>パラメーター


<span id="______________"></span> **+**   
により*TMFPath*既存の検索パスに追加します。 場合は、プラス (+) トークンを使用しない*TMFPath*既存の検索パスに置き換えます。

<span id="_______TMFPath______"></span><span id="_______tmfpath______"></span><span id="_______TMFPATH______"></span> *TMFPath*   
デバッガーはトレース メッセージのフォーマット ファイルを検索するディレクトリへのパス。 空白を含むパスはサポートされていません。 複数のパスが含まれる場合は、セミコロンで区切る必要がありますが、文字列全体を引用符で囲む必要があります。 円記号はエスケープ文字続く必要があります、パスが引用符である場合は、( `"c:\\debuggers;c:\\debuggers2"` )。 ときに、 **+** トークンを使用すると、 *TMFPath*既存のパスと、新しいパスの間に自動的に挿入をセミコロンで既存のパスに追加されるただし場合、 **+** トークンを使用して、引用符を使用することはできません。

<span id="_____________"></span>   

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Wmitrace.dll によってエクスポートされます。

この拡張機能は、Windows 2000 以降のバージョンの Windows で使用できます。 Windows 2000 でこの拡張機能を使用する場合は、w2kfre サブディレクトリに Wmitrace.dll ファイルを Windows 内のデバッグ ツールのインストール ディレクトリの winxp サブディレクトリからまずコピーする必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントのトレースの概念的な概要については、Microsoft Windows SDK を参照してください。 トレース メッセージのフォーマット ファイルについては、Windows Driver Kit (WDK) で「トレース メッセージのフォーマット ファイル」のトピックを参照してください。

<a name="remarks"></a>注釈
-------

パラメーターなしで使用すると **! wmitrace.searchpath**現在の検索パスが表示されます。

トレース メッセージのフォーマット ファイル (\*.tmf) トレース プロバイダーによって生成されるバイナリのトレース メッセージを書式設定するための手順が含まれています。

*TMFPath*パラメーターは、ディレクトリへのパスのみを含める必要があります。 ファイル名を含めることはできません。 TMF ファイルの名前は、メッセージに .tmf 拡張子 GUID です。 システムでは、メッセージを書式設定、ときにメッセージのメッセージの GUID を読み取るし、TMF ファイルの名前には、メッセージには、指定したディレクトリの GUID が一致するには、再帰的に検索します。

Windows では、バッファー内のバイナリ トレース メッセージの書式を設定するには TMF ファイルが必要です。 使用 **! wmitrace.searchpath**または[ **! wmitrace.tmffile** ](-wmitrace-tmffile.md) TMF ファイルを使用する前に指定する[ **! wmitrace.dynamicprint**](-wmitrace-dynamicprint.md)または[ **! wmitrace.logdump** ](-wmitrace-logdump.md)トレース バッファーの内容を表示します。

いずれかを使用しない場合 **! wmitrace.searchpath**または[ **! wmitrace.tmffile**](-wmitrace-tmffile.md)、システムは、トレースの値を使用して\_形式\_検索\_PATH 環境変数。 その変数が存在しない場合は、Windows に含まれている default.tmf ファイルが使用されます。 システムで、トレース メッセージの書式設定情報が見つからない場合は、トレース メッセージの内容の代わりに「の書式情報が見つかりません」エラー メッセージを書き込みます。

 

 





