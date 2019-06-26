---
title: バッテリ情報クエリへの応答
description: バッテリ情報クエリへの応答
ms.assetid: 5d215ff8-d41f-471e-bc54-570a94f3c23f
keywords:
- バッテリ情報 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9eb1df6611596377d8ad2c43a585052287290b0c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355237"
---
# <a name="responding-to-battery-information-queries"></a>バッテリ情報クエリへの応答


## <span id="ddk_responding_to_battery_information_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_INFORMATION_QUERIES_DG"></span>


バッテリ クラス ドライバーの呼び出し、 [ *BatteryMiniQueryInformation* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_information_callback)ルーチンをさまざまな現在のバッテリに関する情報を取得します。 このルーチンは、次のように宣言されます。

```cpp
typedef 
NTSTATUS
(*BCLASS_QUERY_INFORMATION)(
    IN PVOID Context,
    IN ULONG BatteryTag,
    IN BATTERY_QUERY_INFORMATION_LEVEL Level,
    IN LONG AtRate OPTIONAL,
    OUT PVOID Buffer,
    IN ULONG BufferLength,
    OUT PULONG ReturnedLength
    );
```

*コンテキスト*パラメーターは miniclass ドライバーによって割り当てられ、クラス ドライバーに渡されるコンテキスト領域へのポインター、 [**バッテリ\_ミニポート\_情報**](https://docs.microsoft.com/windows/desktop/api/batclass/ns-batclass-battery_miniport_info)デバイスの初期化で構造体。 *BatteryTag*パラメーターは、値によって以前返さ[ *BatteryMiniQueryTag*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)します。

*レベル*パラメーターが要求された情報の種類を指定します。 Miniclass ドライバーとして情報を書式設定、 [**バッテリ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff536283)構造体し、によって提供されるアドレスに返す*バッファー*で、長さへのポインター *ReturnedLength*します。

次の要求を処理する miniclass ドライバーを準備する必要があります。

-   バッテリの機能、化学、容量、容量の小さい警告レベル、および予約の料金

-   10 分の 1 度ケルビンの温度

-   秒単位の残りの実行時の推定

-   デバイス名

-   製造元のバッテリのモデル名

-   製造日

-   一意の ID

-   シリアル番号

いくつかのバッテリは、すべての情報を報告できません。 Miniclass ドライバーは、状態を返す必要があります\_無効な\_デバイス\_要求情報がそのデバイスが提供することはできません。

 

 




