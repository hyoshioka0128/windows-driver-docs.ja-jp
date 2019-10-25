---
title: CLFS ストリームへの再開始レコードの書き込み
description: CLFS ストリームへの再開始レコードの書き込み
ms.assetid: ae341d7e-37b2-4880-948c-e78e29278c64
keywords:
- WDK カーネルの共通ログファイルシステム、レコードの再起動
- CLFS WDK カーネル、再起動レコード
- WDK CLFS レコードの再起動
- チェックポイント WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b9bda9a30f8f80e180c1183dbfa8c20accca299
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835567"
---
# <a name="writing-restart-records-to-a-clfs-stream"></a>CLFS ストリームへの再開始レコードの書き込み





共通ログファイルシステム (CLFS) ストリームには、データレコードと再起動レコードの2種類のレコードがあります。 このトピックでは、CLFS ストリームに再起動レコードを書き込む方法について説明します。 データレコードを書き込む方法については、「 [CLFS ストリームへのデータレコードの書き込み](writing-data-records-to-a-clfs-stream.md)」を参照してください。

通常、再起動レコードは、システム障害が発生した場合の復旧効率を高めるためのチェックポイントを作成するために、定期的にストリームに書き込まれます。 既にマーシャリング領域を作成し、複数のデータレコードを書き込んでいるとします。 その後、 [**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)を呼び出して再起動レコードを作成できます。 *Fflags*パラメーターを設定することにより、再起動レコードをマーシャリング領域の予約領域に配置するか、新しく割り当てられた領域に配置するかを指定できます。CLFS が再起動レコードをストリームに書き込むときに、レコードの前の LSN が、そのストリームに対して以前に書き込まれた再起動レコードの LSN に自動的に設定されます。 これは、逆の順序で走査できる再起動レコードのチェーンを形成します。 再起動レコードのチェーンの詳細については、「 [CLFS ストリームからの再起動レコードの読み取り](reading-restart-records-from-a-clfs-stream.md)」を参照してください。

ストリームに再起動レコードを書き込み、ストリームのベース LSN を同時に変更する場合は、 **ClfsWriteRestartArea**の*plsnbase*パラメーターを新しいベース lsn に設定します。

 

 




