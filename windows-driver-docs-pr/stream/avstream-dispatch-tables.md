---
title: AVStream ディスパッチ テーブル
description: AVStream ディスパッチ テーブル
ms.assetid: 974ea9ee-bb59-4973-83ef-c61f0240a555
keywords:
- ディスパッチテーブル WDK AVStream
- AVStream ディスパッチテーブル WDK
- KSDEVICE_DISPATCH
- 関数のディスパッチ WDK AVStream
- ディスパッチ関数 WDK AVStream
- プロセスディスパッチ WDK AVStream
- フィルター中心のフィルター (WDK AVStream)
- pin 中心のフィルター (WDK AVStream)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2de914039f39aabf52ca65c7fa8a4f4005714ffe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845285"
---
# <a name="avstream-dispatch-tables"></a>AVStream ディスパッチ テーブル





AVStream ディスパッチテーブル ( [**Ksdevice\_dispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_dispatch)) は、ディスパッチ関数への一連の関数ポインターです。 ミニドライバーは、ドライバー固有のタスクを実行するコールバックルーチンを提供することによって、AVStream によって提供される動作を拡張できます。

これらのミニドライバーで提供されるルーチンは、特定のイベントの通知を受け取り、AVStream によって提供される既定のイベント処理を拡張または変更することができます。

[**Ksfilter\_dispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)と[**kspin\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)構造体はどちらも、 *Process*と呼ばれるディスパッチを提供します。 [フィルター中心](filter-centric-processing.md)のフィルターを[ピン中心](pin-centric-processing.md)のフィルターと区別するには、このディスパッチを使用します。フィルター中心のフィルターを指定するには、フィルターディスパッチテーブルのプロセスディスパッチコールバックルーチンへのポインターを指定します。 ピン中心のフィルターでは、各ピン記述子テーブルにプロセスディスパッチが用意されています。

フィルターを登録して、作成、削除、データ処理の必要性、およびリセットに関する通知を受け取ることができます。 Pin を登録して、作成、終了、データの処理、リセット、データ形式の設定、状態の変更などのイベントを通知することができます。 オブジェクトを通知用に登録するには、関連するディスパッチ構造体で、ベンダーが提供するディスパッチルーチンへのポインターを指定します。

ディスパッチ関数の詳細については、「 [**Ksfilter\_dispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)」、「 [**KSPIN\_dispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)」、および「 [**ksallocator\_dispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksallocator_dispatch)」を参照してください。

 

 




