---
title: IRP_MJ_FILE_SYSTEM_CONTROL
description: IRP_MJ_FILE_SYSTEM_CONTROL
ms.assetid: 38b88379-c007-4e88-a6d9-5aacd6bdefd3
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL
- セキュリティ WDK ファイル システム、セキュリティ チェックを追加します。
- セキュリティは、WDK のファイル システム、IRP_MJ_FILE_SYSTEM_CONTROL を確認します。
- ファイル システムのコントロールの WDK セキュリティ
- ファイル情報処理 WDK ファイル システムを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67c1808a9aa5c250814b7aea834acd0c48df8e13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573256"
---
# <a name="irpmjfilesystemcontrol"></a>IRP_MJ_FILE_SYSTEM_CONTROL


ファイル システムのコントロールには、基本的には任意の特殊な操作を実行するファイル システムができます。 ファイル システム、および Windows 用に開発されたすべてのサード パーティ製のファイル システムの特殊なコントロールの数がある既存の Windows を積極的にすべてのパラメーターを確認する必要があります。 さらに、FSCTL 操作多くの場合、制限のセキュリティ権限。 これらは、WDK を含む FASTFAT サンプル コードで確認できます (を参照してください、 **FatInvalidateVolumes** fsctrl.c、関数など)。 これは、権限チェックの例です。 FASTFAT ファイル システムのポリシーは、特定の権限が、システムで有効にすることを要求するこの場合は。

I/O マネージャーが、FSCTL の特定の操作で FILE_READ_DATA および FILE_WRITE_DATA アクセス許可をファイル システムが CTL_CODE マクロを使用してファイル システム操作の定義でこれらのビットを設定する場合に適用されます。 必要なその他のすべての権限をチェックする必要があります、ファイル システム (たとえば FILE_READ_ATTRIBUTES 権限) でこれがファイル システムのポリシーの場合。

 

 




