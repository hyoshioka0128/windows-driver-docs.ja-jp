---
title: IRP_MJ_FILE_SYSTEM_CONTROL (IFS)
description: IRP_MJ_FILE_SYSTEM_CONTROL
ms.assetid: 38b88379-c007-4e88-a6d9-5aacd6bdefd3
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL
- セキュリティ WDK ファイルシステム、セキュリティチェックの追加
- セキュリティチェック WDK ファイルシステム、IRP_MJ_FILE_SYSTEM_CONTROL
- ファイルシステムが WDK セキュリティを制御する
- WDK ファイルシステムを処理するファイル情報の設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c24f95c9e2c813dc3aff1e439ecbbdeee6c2ba9c
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141226"
---
# <a name="irp_mj_file_system_control-ifs"></a>IRP_MJ_FILE_SYSTEM_CONTROL (IFS)


ファイルシステムコントロールを使用すると、ファイルシステムは基本的に特化された操作を実行できます。 既存の Windows ファイルシステムには、いくつかの特殊な制御があります。また、Windows 用に開発されたサードパーティのファイルシステムでも、すべてのパラメーターを積極的に確認することが不可欠です。 また、FSCTL 操作には、多くの場合、制限付きのセキュリティ権限があります。 これらは、WDK に含まれる FASTFAT サンプルコードで確認できます (例については、fsctrl の**FatInvalidateVolumes**関数を参照してください)。 これは、特権チェックの一例です。 この場合、FASTFAT ファイルシステムのポリシーは、指定された特権がシステムで有効になっていることを要求します。

ファイルシステムが CTL_CODE マクロを使用してファイルシステム操作の定義でこれらのビットを設定している場合、i/o マネージャーは、特定の FSCTL 操作に対して FILE_READ_DATA および FILE_WRITE_DATA のアクセス許可を適用します。 ファイルシステムのポリシーの場合は、ファイルシステムによって必要なその他すべてのアクセス許可 (FILE_READ_ATTRIBUTES アクセス許可など) を確認する必要があります。

 

 




