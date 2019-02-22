---
title: バッテリ情報のクエリに応答してください。
description: バッテリ情報のクエリに応答してください。
ms.assetid: 5d215ff8-d41f-471e-bc54-570a94f3c23f
keywords:
- バッテリ情報 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b003b90dd145dae7c8f820c097925a8d9b77e795
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557098"
---
# <a name="responding-to-battery-information-queries"></a>バッテリ情報のクエリに応答してください。


## <span id="ddk_responding_to_battery_information_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_INFORMATION_QUERIES_DG"></span>


バッテリ クラス ドライバーの呼び出し、 [ *BatteryMiniQueryInformation* ](https://msdn.microsoft.com/library/windows/hardware/ff536273)ルーチンをさまざまな現在のバッテリに関する情報を取得します。 このルーチンは、次のように宣言されます。

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

*コンテキスト*パラメーターは miniclass ドライバーによって割り当てられ、クラス ドライバーに渡されるコンテキスト領域へのポインター、 [**バッテリ\_ミニポート\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff536287)デバイスの初期化で構造体。 *BatteryTag*パラメーターは、値によって以前返さ[ *BatteryMiniQueryTag*](https://msdn.microsoft.com/library/windows/hardware/ff536275)します。

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

 

 




