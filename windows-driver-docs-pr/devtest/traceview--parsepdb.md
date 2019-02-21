---
title: Traceview で parsepdb
description: Traceview で - parsepdb コマンドを使用すると、PDB シンボル ファイル内のデータからトレース メッセージのフォーマット ファイルを作成できます。
ms.assetid: d193aa3c-17ee-4fcf-a4ee-afb50c78ec54
keywords:
- Traceview で - parsepdb ドライバーの開発ツール
topic_type:
- apiref
api_name:
- TraceView -parsepdb
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86e176fc5e92cc7166c492ee8ebd2d63d3967040
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539422"
---
# <a name="traceview--parsepdb"></a>Traceview で parsepdb

使用して、 **traceview で parsepdb**を作成するコマンド[トレース メッセージの形式のファイル](trace-message-format-file.md)内のデータから、 [PDB シンボル ファイル](pdb-symbol-files.md)します。

```
    traceview -parsepdb PDBfile [-p TMFPath] 
   
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______PDBfile______"></span><span id="_______pdbfile______"></span><span id="_______PDBFILE______"></span> *PdbFile*   
PDB シンボル ファイルのパスとファイル名を指定します。

<span id="_______-p_______TMFPath______"></span><span id="_______-p_______tmfpath______"></span><span id="_______-P_______TMFPATH______"></span> **-p** *TMFPath*   
トレース メッセージの形式 (TMF) ファイルのディレクトリを指定します。

TMF ファイルの名前を指定することはできません。 ファイル名は、 [GUID をメッセージ](message-guid.md)トレース プロバイダーの。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

```
traceview -parsepdb tracedrv.pdb
traceview -parsepdb tracedrv.pdb -p d:\tracing
```

コメント

Traceview でも作成、[トレース メッセージのコントロール (.tmc) ファイル](trace-message-control-file.md)ごと[トレース プロバイダー](trace-provider.md)ソース コードにします。 TMC ファイルが含まれています、[コントロール GUID](control-guid.md)と PDB ファイルで表される各トレース プロバイダーのトレース レベル。 TMC ファイルの名前は、コントロールのトレース プロバイダーの GUID です。

Traceview で応答する場合、 **- parsepdb**コマンドを表示するだけで、**を終了する任意のキーを押して**メッセージ、必要な DLL がディレクトリに移動されていないこと可能性があります、traceview でtraceview.exe を実行可能ファイルが配置されています。 詳細については、次を参照してください。 [traceview での使用の準備](preparing-to-use-traceview.md)します。 これも可能性が PDB ファイルには、トレースの必要なコンポーネントがありません。 PDB ファイルの作成元のソース コードがソフトウェア トレースに対してインストルメント化されていることを確認します。
