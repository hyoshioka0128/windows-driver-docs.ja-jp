---
title: チェンジャークラスのドライバーについて
description: チェンジャー クラス ドライバー
ms.assetid: c1c2330c-9cfc-432f-945c-630dc16aa54d
keywords:
- チェンジャードライバー WDK storage、クラスドライバー
- storage チェンジャードライバー WDK、クラスドライバー
- クラスドライバー WDK storage、チェンジャードライバー
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2eb702868f6d50d2245ebff48c1c90c79c7735b5
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606540"
---
# <a name="about-the-changer-class-driver"></a>チェンジャークラスのドライバーについて

システム指定のチェンジャークラスドライバーは、ハードウェアベンダーによって提供されるチェンジャー miniclass ドライバーに対して、オペレーティングシステム固有のデバイスに依存しないサービスを実行します。 チェンジャー miniclass ドライバーの詳細については、「[チェンジャー Miniclass ドライバー](introduction-to-changer-miniclass-drivers.md)」を参照してください。

チェンジャークラスドライバー:

- Miniclass ドライバーがプールメモリの割り当てと解放を行うために呼び出すメモリ割り当てルーチンを提供します。

- オペレーティングシステムに依存しない、Microsoft Windows XP 以降のオペレーティングシステムのポートドライバーに同期 SRBs を送信する方法を提供します (Windows 2000 と Windows XP の違いについては、「[チェンジャークラスドライバーのバージョンの違い](differences-in-changer-class-driver-versions.md)」を参照してください)。

- クラス/miniclass ドライバーペアの初期化に役立ちます。

- **チェンジャー * * * Xxx* miniclass ドライバールーチンを呼び出して、デバイス固有の情報に割り当てる領域の量を決定し、他の要求を受信するようにチェンジャーを準備します。

- [**IRP_MJ_DEVICE_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求に対してデバイスに依存しないプリプロセスを実行し、適切な **チェンジャー * * * Xxx* miniclass ルーチンを呼び出して、要求を完了します。

- デバイスに依存しないプリプロセスを実行してエラーを処理し、デバイス固有の処理のために miniclass ドライバーの[**Changererror**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changererror)ルーチンを呼び出します。

- **チェンジャー * * * Xxx* miniclass ドライバールーチンを呼び出して、製品データを取得したり、要素の状態を変更したり、クエリまたはボリュームタグのデータを照会したりします。
