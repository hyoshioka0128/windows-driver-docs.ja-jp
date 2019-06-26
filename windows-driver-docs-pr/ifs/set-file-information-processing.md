---
title: ファイル情報設定処理
description: ファイル情報設定処理
ms.assetid: bda94e8d-0be1-4730-a82e-4aa4d3763cce
keywords:
- WDK ファイル システムのセキュリティ、セマンティック モデルを確認します
- セマンティック モデルには WDK ファイル システムがチェックされ、ファイル情報の処理の設定
- ファイル情報処理 WDK ファイル システムを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf9d2fb2a3d3ba376c1b325c7b0266babc408c2c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359263"
---
# <a name="set-file-information-processing"></a>ファイル情報設定処理


## <span id="ddk_set_file_information_processing_if"></span><span id="DDK_SET_FILE_INFORMATION_PROCESSING_IF"></span>


サポートされている情報クラスのサブセットのいくつか追加のチェックを実行する I/O マネージャー [ **IRP\_MJ\_設定\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-information)します。 具体的には、FileRenameInformation、FileLinkInformation および FileMoveClusterInformation、I/O マネージャー問題のオープン送信するには、その親の下に子を作成するアクセスをユーザーが持っていることを確認する対象の名前の親ディレクトリに、IRP\_MJ\_設定\_ファイル システムに情報の要求。

 

 




