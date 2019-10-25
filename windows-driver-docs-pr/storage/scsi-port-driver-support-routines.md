---
title: SCSI ポート ドライバーのサポート ルーチン
description: SCSI ポートドライバールーチンについて説明します。
ms.assetid: b4bd6afe-77a2-4bd1-a762-5887f77cc737
keywords:
- SCSI ポートドライバーのサポートルーチン
- ストレージ WDK
- ストレージサポートルーチン
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8a85086f7196393e162c6d6693aca1956601c2ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842658"
---
# <a name="scsi-port-driver-support-routines"></a>SCSI ポート ドライバーのサポート ルーチン

オペレーティングシステム固有の SCSI ポートドライバーには、オペレーティングシステムに依存しないオペレーティングシステム固有の scsi ポートドライバーにリンクされているオペレーティングシステムに依存しない SCSI ミニポートドライバーをサポートする*ScsiPortXxx*ルーチンが用意されています。 SCSI ポートドライバーは、カーネルモードのダイナミックリンクライブラリです。

*ScsiPortXxx*ルーチンの一覧と参照ページは次の場所にあります。

| ルーチン | Header |
| ------- | ------- |
| *ScsiPortXxx* | [srb ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/) |
| *ScsiPortWmiXxx* | [scsiwmi](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/) |

SCSI ミニポートドライバールーチンの一覧については、「 [Scsi ミニポートドライバールーチン](scsi-miniport-driver-routines.md)」を参照してください。
