---
title: CLFS ストリームからの再開始レコードの読み取り
description: CLFS ストリームからの再開始レコードの読み取り
ms.assetid: 310545f6-d10d-481e-829d-287b045b98cd
keywords:
- 一般的なログ ファイル システムの WDK カーネル、再開レコード
- CLFS WDK カーネル、再開レコード
- レコード WDK CLFS を再起動します。
- 読み取り再開レコード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a454aeb3dc38c15dd322dcfb139f6e56638bf258
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382650"
---
# <a name="reading-restart-records-from-a-clfs-stream"></a>CLFS ストリームからの再開始レコードの読み取り





(逆の順序で) 再起動 Common Log File System (CLFS) ストリーム内のすべて読み取りするには、次の手順を使用します。

1.  呼び出す[ **ClfsReadRestartArea** ](https://msdn.microsoft.com/library/windows/hardware/ff541709)読み取りコンテキストとストリームに書き込まれた最も最近再開レコードを取得します。

2.  手順 1 で取得した読み取りコンテキストを渡す[ **ClfsReadPreviousRestartArea** ](https://msdn.microsoft.com/library/windows/hardware/ff541699)繰り返し取得する残りのレコードで再起動ログ。

**注**  を呼び出すと[ **ClfsWriteRestartArea** ](https://msdn.microsoft.com/library/windows/hardware/ff541770)をストリームには、再開レコードを書き込む、CLFS に自動的に設定以前そのレコードの LSN の以前の LSNストリーム内のレコードを再起動します。 これらの以前の Lsn は、繰り返しの呼び出しが続くチェーンを形成**ClfsReadPreviousRestartArea**します。

 

 

 




