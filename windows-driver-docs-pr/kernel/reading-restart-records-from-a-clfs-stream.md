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
ms.openlocfilehash: ffe2dc6ce2237c561d18a8715534d37067541da4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378758"
---
# <a name="reading-restart-records-from-a-clfs-stream"></a>CLFS ストリームからの再開始レコードの読み取り





(逆の順序で) 再起動 Common Log File System (CLFS) ストリーム内のすべて読み取りするには、次の手順を使用します。

1.  呼び出す[ **ClfsReadRestartArea** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadrestartarea)読み取りコンテキストとストリームに書き込まれた最も最近再開レコードを取得します。

2.  手順 1 で取得した読み取りコンテキストを渡す[ **ClfsReadPreviousRestartArea** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadpreviousrestartarea)繰り返し取得する残りのレコードで再起動ログ。

**注**  を呼び出すと[ **ClfsWriteRestartArea** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfswriterestartarea)をストリームには、再開レコードを書き込む、CLFS に自動的に設定以前そのレコードの LSN の以前の LSNストリーム内のレコードを再起動します。 これらの以前の Lsn は、繰り返しの呼び出しが続くチェーンを形成**ClfsReadPreviousRestartArea**します。

 

 

 




