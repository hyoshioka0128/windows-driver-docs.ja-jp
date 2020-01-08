---
title: 記憶域フィルター ドライバーのデバイスの種類に固有な機能
description: 記憶域フィルター ドライバーのデバイスの種類に固有な機能
ms.assetid: ecc0d938-e931-46bd-a1e1-0e6da8e149a4
keywords:
- ストレージフィルタードライバー WDK、デバイスタイプ固有の機能
- フィルタードライバー WDK storage、デバイスタイプ固有の機能
- SFD WDK storage、デバイスタイプ固有の機能
- デバイスタイプ固有の機能 WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 188c31d95d6720dd45edef8e7551f462ccee97df
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606440"
---
# <a name="storage-filter-drivers-device-type-specific-functionality"></a>記憶域フィルター ドライバーのデバイスの種類に固有な機能

デバイスの性質によっては、次のデバイスの種類に固有の機能をストレージフィルタードライバー (SFD) が担当する場合があります。

- デバイスが非標準形式でデータを処理する場合に、転送要求を下位ドライバーに送信する前または後に、デバイス固有の形式との間でデータを変換する

- ポートドライバーでサポートされている i/o 制御要求、ドライバー定義の i/o 制御要求、またはデバイスに必要なパススルー要求に対して SRBs を使用して Irp を設定し、それらの Irp を次の下位のドライバーに送信します。

- デバイスの必要に応じて、クラスドライバーが提供する SRBs を変更する

- 要求のタイムアウト値の設定

- 1つ以上の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを提供し、対応するストレージクラスドライバーと同様に、特定のエラー状態を処理し、特別な処理を必要とするデバイス固有の要求の再試行を行います。

一般に、SFD は、デバイス固有の処理を必要とする要求に対して、ストレージクラスドライバーと同じ役割を持ちます。 ストレージクラスドライバーに必要な機能の詳細については、「[ストレージクラスドライバー](introduction-to-storage-class-drivers.md)」を参照してください。
