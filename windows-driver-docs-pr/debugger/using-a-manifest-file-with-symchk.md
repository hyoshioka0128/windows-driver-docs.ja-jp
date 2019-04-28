---
title: SymChk でのマニフェスト ファイルの使用
description: SymChk でのマニフェスト ファイルの使用
ms.assetid: ee5d0c39-1838-4595-adf4-6cd1261a57c8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7db76f75ecab5769c2ce33554f3c5500b247fdc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367968"
---
# <a name="using-a-manifest-file-with-symchk"></a>SymChk でのマニフェスト ファイルの使用


## <span id="ddk_using_symchk_dtoolq"></span><span id="DDK_USING_SYMCHK_DTOOLQ"></span>


場合によっては、分離、コンピューター上にあるファイルのシンボルを取得する必要があります。ないか、コンピューターは、ネットワーク上をシンボル ストアを持たないネットワーク上にあるか。 そのような状況では、シンボルを取得するのに、次の手順を使用できます。

1.  SymChk での実行、 **/om**パラメーター シンボルを取得するファイルを記述するマニフェスト ファイルを作成します。

2.  シンボル ストアを持つネットワークにマニフェスト ファイルを移動します。

3.  SymChk での実行、 **/im**マニフェスト ファイルで説明されているファイルのシンボルを取得するパラメーター。

4.  シンボル ファイルを孤立したコンピューターに移動します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

たとえば、yourApp.exe が分離されたコンピューターで実行されています。 次のコマンドは、yourApp.exe pocess をデバッグするために必要なすべてのシンボルを記述するマニフェスト ファイルを作成します。

```dbgcmd
C:\>SymChk /om c:\Manifest\man.txt /ie yourApp.exe

SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 28
```

今すぐシンボル ストアにアクセスできるネットワーク上にある別のコンピューターに、マニフェスト ファイルを移動すると仮定します。 次のコマンドは、マニフェスト ファイルで説明されているシンボルを取得し、mySymbols フォルダーに配置します。

```dbgcmd
C:\>SymChk /im c:\FolderOnOtherComputer\man.txt /s srv*c:\mysymbols*\\aServer\symbols

SYMCHK: myApp.exe             ERROR - Unable to download file. Error reported was 2
. . .
SYMCHK: FAILED files = 28
SYMCHK: PASSED + IGNORED files = 28
```

孤立したコンピューターに、シンボルの移動をデバッグするために使用できます。

 

 





