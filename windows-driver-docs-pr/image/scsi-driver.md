---
title: SCSI ドライバー
description: SCSI ドライバー
ms.assetid: e69e3ac6-6726-4f63-afdb-2da1255dde19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 088a3c14cb6d00f513284350aa03c12862c1c2d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374252"
---
# <a name="scsi-driver"></a>SCSI ドライバー





SCSI の静止画像カーネル モード ドライバー サポートのバス**ReadFile** SCSI を含むコマンド記述子ブロック (CDB) を作成して**読み取り**コマンド。 サポート**WriteFile** SCSI を含む CDB を作成して**書き込み**コマンド。 ユーザー モードのミニドライバーは、呼び出すことによってカスタマイズされた Cdb を指定できます[ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)します。 詳細については、次を参照してください。 [SCSI まだイメージ I/O 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)します。 Microsoft Windows SDK ドキュメントの説明を参照して**ReadFile**と**WriteFile**します。

 

 




