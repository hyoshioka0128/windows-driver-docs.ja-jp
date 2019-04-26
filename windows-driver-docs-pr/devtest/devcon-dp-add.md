---
title: DevCon Dp_add
description: ローカル コンピューターのドライバー ストアにサード パーティ (OEM) のドライバー パッケージを追加します。
ms.assetid: 929bb59b-f227-47c5-9351-270ffbe4d745
keywords:
- DevCon Dp_add ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Dp_add
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46ec3c6cd36251e9f8de30964909f074e333558b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353938"
---
# <a name="devcon-dpadd"></a>DevCon Dp\_追加


ローカル コンピューターのドライバー ストアにサード パーティ (OEM) のドライバー パッケージを追加します。

```
    devcon dp_add inf
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______inf______"></span><span id="_______INF______"></span> *inf*   
完全修飾パスと、ドライバー パッケージの INF ファイルの名前。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

DevCon dp\_コマンド %windir%/Inf ディレクトリに指定した INF ファイルをコピーし、OEM は名前に変更を追加\*。 inf します。 このファイル名は、コンピューター上で一意と指定することはできません。

INF ファイルが、%windir%/Inf にないコピーし直さなくて %windir%/Inf (一致するファイル名ではなく、バイナリ ファイルを比較することで決定された) ように、この INF ファイルが既に存在します、INF のカタログ (.cat) ファイルは、ディレクトリ内のカタログ ファイルと同じ場合は、ディレクトリ。

このコマンドを呼び出す、 **SetupCopyOEMInf**のない関数*CopyStyle*フラグ。 **SetupCopyOEMInf**については、Microsoft Windows SDK ドキュメントで説明します。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon dp_add C:\WinDDK\5322\src\general\toaste
r\inf\i386\toaster.inf
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[45 の使用例:追加して、ドライバー パッケージを削除します。](example-45--add-and-remove-driver-packages.md)









