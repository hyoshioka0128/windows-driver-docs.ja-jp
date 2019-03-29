---
title: SCSI ドライバー
description: SCSI ドライバー
ms.assetid: e69e3ac6-6726-4f63-afdb-2da1255dde19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10af337182a63a149f3b446c4ab310300d52f059
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572092"
---
# <a name="scsi-driver"></a>SCSI ドライバー





SCSI の静止画像カーネル モード ドライバー サポートのバス**ReadFile** SCSI を含むコマンド記述子ブロック (CDB) を作成して**読み取り**コマンド。 サポート**WriteFile** SCSI を含む CDB を作成して**書き込み**コマンド。 ユーザー モードのミニドライバーは、呼び出すことによってカスタマイズされた Cdb を指定できます[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)します。 詳細については、次を参照してください。 [SCSI まだイメージ I/O 制御コード](https://msdn.microsoft.com/library/windows/hardware/ff548003)します。 Microsoft Windows SDK ドキュメントの説明を参照して**ReadFile**と**WriteFile**します。

 

 




