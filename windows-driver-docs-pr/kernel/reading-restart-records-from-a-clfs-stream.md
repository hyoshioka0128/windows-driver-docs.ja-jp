---
title: CLFS ストリームからの再開始レコードの読み取り
description: CLFS ストリームからの再開始レコードの読み取り
ms.assetid: 310545f6-d10d-481e-829d-287b045b98cd
keywords:
- WDK カーネルの共通ログファイルシステム、レコードの再起動
- CLFS WDK カーネル、再起動レコード
- WDK CLFS レコードの再起動
- 再開レコードの読み取り
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8400c08bd37c8648e53a76abbe015e4f392d18f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827576"
---
# <a name="reading-restart-records-from-a-clfs-stream"></a>CLFS ストリームからの再開始レコードの読み取り





共通ログファイルシステム (CLFS) ストリームのすべての再起動レコードを逆の順序で読み取るには、次の手順に従います。

1.  [**ClfsReadRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadrestartarea)を呼び出して、最後にストリームに書き込まれた読み取りコンテキストと再起動レコードを取得します。

2.  手順 1. で取得した読み取りコンテキストを[**ClfsReadPreviousRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadpreviousrestartarea)に渡して、ログ内の残りの再起動レコードを取得します。

  **メモ** [**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)を呼び出してストリームに再起動レコードを書き込むと、CLFS は、そのレコードの前の lsn をストリーム内の前の再起動レコードの lsn に自動的に設定します。 これらの前の Lsn は、 **ClfsReadPreviousRestartArea**を繰り返し呼び出すチェーンを形成します。

 

 

 




