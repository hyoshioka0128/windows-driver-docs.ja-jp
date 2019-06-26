---
title: CLFS ストリームへの再開始レコードの書き込み
description: CLFS ストリームへの再開始レコードの書き込み
ms.assetid: ae341d7e-37b2-4880-948c-e78e29278c64
keywords:
- 一般的なログ ファイル システムの WDK カーネル、再開レコード
- CLFS WDK カーネル、再開レコード
- レコード WDK CLFS を再起動します。
- チェックポイント WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb67d97a8dcb0a44b3dcd71a602e9b1b92a1afcf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374108"
---
# <a name="writing-restart-records-to-a-clfs-stream"></a>CLFS ストリームへの再開始レコードの書き込み





Common Log File System (CLFS) ストリーム内のレコードの 2 種類があります。 データがレコードとレコードを再起動します。 このトピックでは、CLFS ストリームに再開レコードを書き込む方法について説明します。 データ レコードを作成する方法については、次を参照してください。 [CLFS Stream へのデータ レコードの書き込み](writing-data-records-to-a-clfs-stream.md)します。

通常、再開レコードが書き込まれますをストリームに定期的にシステム障害時復旧をより効率的な実現をサポートするチェックポイントを作成します。 既にマーシャ リング領域を作成している複数のデータ レコードが書き込まれると仮定します。 呼び出すことによって再開レコードを作成し、 [ **ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfswriterestartarea)します。 設定して、 *fFlags*パラメーター マーシャ リング領域の予約領域か、新しく割り当てられた領域に再開レコードを配置するかどうか指定できます。CLFS は、再開レコードをストリームに書き込む、ときに自動的に、そのストリームの以前に書き込まれた再開レコードの LSN を前のレコードの LSN を設定します。 逆の順序で走査できる再起動レコードのチェーンを形成します。 再起動のレコードのチェーンを読み込む方法の詳細については、次を参照してください。 [CLFS Stream から読み取りを再開レコード](reading-restart-records-from-a-clfs-stream.md)します。

再開レコードをストリームに書き込むし、同時にストリームのベース LSN を変更する場合は、設定、 *plsnBase*パラメーターの**ClfsWriteRestartArea**を新しいベース LSN。

 

 




