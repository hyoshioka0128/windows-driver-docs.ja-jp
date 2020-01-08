---
title: ATA ポート i/o モデルの概要
description: ATA ポート i/o モデルの概要
ms.assetid: 6feaf2c4-63b2-4ab2-9d4d-7259406be652
keywords:
- ATA ポートドライバー WDK、i/o
- I/o WDK ATA ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f62ba5d199613ebc663315c53a2e8e2e9acea45
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606494"
---
# <a name="ata-port-io-model-overview"></a>ATA ポート i/o モデルの概要

> [!NOTE]
> ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。

ATA ポートドライバーは、Storport ドライバーと同様に、i/o のプッシュモデルを使用します。 これは、ドライバーが i/o 要求をミニポートドライバーに非同期で転送することを意味します。これは、ミニポートドライバーが入力を要求するのを待たずに、重複するパケットの最大数になります。 プッシュモデルでは、ポートドライバーは i/o 要求のフローを制御し、要求をミニポートドライバーにプッシュします。

一方、SCSI ポートドライバーは、i/o のプルモデルを使用します。 I/o のプルモデルでは、SCSI ポートドライバーはミニポートドライバーに i/o 要求を同期的に転送し、次の i/o 要求を送信する前にミニポートドライバーが新しい入力を要求するまで待機します。 さらに、ミニポートドライバーは、i/o 要求のフローを制御し、ポートドライバーから要求を取得します。

Storport ドライバーの i/o モデルの詳細については、「 [storport I/o モデル](storport-i-o-model.md)」を参照してください。

SCSI ポートドライバーの i/o モデルの詳細については、「 [Scsi ポート I/o モデル](scsi-port-i-o-model.md)」を参照してください。
