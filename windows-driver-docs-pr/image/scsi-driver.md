---
title: SCSI ドライバー
description: SCSI ドライバー
ms.assetid: e69e3ac6-6726-4f63-afdb-2da1255dde19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70706845b4bec3cb4203dd83632c33d03c1f4260
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840751"
---
# <a name="scsi-driver"></a>SCSI ドライバー





SCSI バス用のカーネルモード静止イメージドライバーは、SCSI**読み取り**コマンドを含むコマンド記述子ブロック (CDB) を作成することによって、 **ReadFile**をサポートします。 また、SCSI**書き込み**コマンドを含む CDB を作成することによって、 **WriteFile**をサポートしています。 ユーザーモードミニドライバーでは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を呼び出すことで、カスタマイズされた cdbs を指定できます。 詳細については、「 [SCSI のイメージ I/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)」を参照してください。 **ReadFile**と**WriteFile**の説明については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




