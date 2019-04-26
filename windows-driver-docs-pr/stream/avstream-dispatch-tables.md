---
title: AVStream ディスパッチ テーブル
description: AVStream ディスパッチ テーブル
ms.assetid: 974ea9ee-bb59-4973-83ef-c61f0240a555
keywords:
- ディスパッチ テーブル WDK AVStream
- AVStream ディスパッチ テーブル WDK
- KSDEVICE_DISPATCH
- WDK AVStream のディスパッチ関数
- WDK AVStream のディスパッチ関数
- WDK AVStream のディスパッチを処理します。
- フィルターを中心としたフィルター WDK AVStream
- 暗証番号 (pin) を中心としたフィルター WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9e06d7c0829e50e86d6cee510d43bab4def383c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352618"
---
# <a name="avstream-dispatch-tables"></a>AVStream ディスパッチ テーブル





AVStream のディスパッチ テーブル[ **KSDEVICE\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff561693)関数にディスパッチ関数ポインターのセットです。 ミニドライバーは、ドライバー固有のタスクを実行するコールバック ルーチンを提供することで、AVStream によって提供される動作を拡張できます。

これらのミニドライバーのルーチンは現在特定のイベントの通知を受信および拡張、または AVStream によって提供される既定のイベント処理を変更可能性があります。

両方[ **KSFILTER\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff562554)と[ **KSPIN\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff563535)構造体と呼ばれるディスパッチを提供します。*プロセス*します。 このディスパッチを使用して区別する、[フィルターを中心とした](filter-centric-processing.md)からフィルター処理、[暗証番号 (pin) を中心とした](pin-centric-processing.md)フィルター。フィルターを中心としたフィルターを指定するには、フィルターのディスパッチ テーブルでプロセスのディスパッチ コールバック ルーチンへのポインターを指定します。 暗証番号 (pin) を中心としたフィルターは、暗証番号 (pin) の記述子テーブルの各プロセスのディスパッチを提供します。

作成、削除、データ、およびリセットを処理する必要を通知するフィルターを登録できます。 データ形式、および状態の変更の設定のピンはクロージャでは、データを処理する必要がリセットされ、作成などのイベントの通知を登録できます。 通知オブジェクトを登録するには、適切なディスパッチ構造内のベンダーから提供されたディスパッチ ルーチンへのポインターを指定します。

ディスパッチ関数の詳細については、次を参照してください[ **KSFILTER\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff562554)、 [ **KSPIN\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff563535)。、および[ **KSALLOCATOR\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff560976)します。

 

 




