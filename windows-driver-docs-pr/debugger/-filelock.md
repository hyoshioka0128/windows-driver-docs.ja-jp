---
title: filelock
description: Filelock 拡張機能は、ファイルのロック構造を表示します。
ms.assetid: 943a0ed8-b7a5-4ab6-8579-6a27e06e1dac
keywords:
- Windows デバッグ filelock
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- filelock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d17027482c4a1ca471c7b8abeab57d8999bd6b5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336728"
---
# <a name="filelock"></a>!filelock


**! Filelock**拡張機能は、ファイルのロック構造を表示します。

構文

```dbgcmd
!filelock FileLockAddress 
!filelock ObjectAddress 
```

## <a name="span-idddkfilelockdbgspanspan-idddkfilelockdbgspanparameters"></a><span id="ddk__filelock_dbg"></span><span id="DDK__FILELOCK_DBG"></span>パラメーター


<span id="_______FileLockAddress______"></span><span id="_______filelockaddress______"></span><span id="_______FILELOCKADDRESS______"></span> *FileLockAddress*   
ファイルのロック構造の 16 進数のアドレスを指定します。

<span id="_______ObjectAddress______"></span><span id="_______objectaddress______"></span><span id="_______OBJECTADDRESS______"></span> *ObjectAddress*   
ファイル ロックを所有するファイル オブジェクトの 16 進数のアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ファイル オブジェクトについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。

 

 





