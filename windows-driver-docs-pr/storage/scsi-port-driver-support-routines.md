---
title: SCSI ポートドライバーのサポートルーチン
description: SCSI ポートドライバールーチンについて説明します。
ms.assetid: b4bd6afe-77a2-4bd1-a762-5887f77cc737
keywords:
- SCSI ポートドライバーのサポートルーチン
- ストレージ WDK
- ストレージサポートルーチン
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9fb49c0671ea1764944edafbc8518740ee3364ce
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72256324"
---
# <a name="scsi-port-driver-support-routines"></a>SCSI ポートドライバーのサポートルーチン

オペレーティングシステム固有の SCSI ポートドライバーには、オペレーティングシステムに依存しないオペレーティングシステム固有の scsi ポートドライバーにリンクされているオペレーティングシステムに依存しない SCSI ミニポートドライバーをサポートする*ScsiPortXxx*ルーチンが用意されています。 SCSI ポートドライバーは、カーネルモードのダイナミックリンクライブラリです。

*ScsiPortXxx*ルーチンの一覧と参照ページは次の場所にあります。

| ルーチン | Header |
| ------- | ------- |
| *ScsiPortXxx* | [srb ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/) |
| *ScsiPortWmiXxx* | [scsiwmi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/) |

SCSI ミニポートドライバールーチンの一覧については、「 [Scsi ミニポートドライバールーチン](scsi-miniport-driver-routines.md)」を参照してください。
