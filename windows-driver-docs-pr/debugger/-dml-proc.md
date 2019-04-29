---
title: dml_proc
description: Dml_proc 拡張機能では、プロセスの一覧を表示し、プロセスに関するより詳細な情報を取得するためのリンクを提供します。
ms.assetid: 35B5B2E7-07CE-4F44-819D-9B7C76273F9A
keywords:
- Windows デバッグ dml_proc
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dml_proc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b95722679652d383f221ce59db5126829ba42edf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334578"
---
# <a name="dmlproc"></a>!dml\_proc


**! Dml\_proc**拡張機能はプロセスの一覧を表示し、プロセスに関するより詳細な情報を取得するためのリンクを提供します。

```dbgcmd
!dml_proc
```

<a name="remarks"></a>注釈
-------

次の図は、によって表示される出力の一部を示しています。 **! dml\_proc**します。

![スクリーン ショット dml\-proc 出力。](images/dmlproc01.png)

上記の出力では、プロセスのアドレスはリンクをクリックするより詳細な情報を参照してください。 たとえばをクリックする**fffffa80\`04e2b700** (mobsync.exe のアドレス)、次の図のように、mobsync.exe プロセスに関する詳細情報が表示されます。

![プロセスの詳細のスクリーン ショット](images/dmlproc02.png)

上記の出力など、個々 のプロセスを説明するには、プロセスとそのスレッドをさらに詳しく調査するクリックできるリンクが含まれています。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[デバッガーのマークアップ言語コマンド](debugger-markup-language-commands.md)

 

 






