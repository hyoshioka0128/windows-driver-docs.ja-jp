---
title: Microsoft 熱拡張機能に対するデバイス固有のメソッド
description: 温度のゾーンと温度センサーのより柔軟なデザインをサポートするためには、Windows は、ACPI 熱ゾーン モデルの拡張機能をサポートします。
ms.assetid: A8D90493-EE4A-40EC-BE8D-54B1C9EE94AD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b031314b9342fcd19178af164269c4814263478
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364564"
---
# <a name="device-specific-method-for-microsoft-thermal-extensions"></a>Microsoft 熱拡張機能に対するデバイス固有のメソッド


温度のゾーンと温度センサーのより柔軟なデザインをサポートするためには、Windows は、ACPI 熱ゾーン モデルの拡張機能をサポートします。 具体的には、Windows では、温度ゾーンごとに温度の最小スロットルの制限 (MTL) をサポートしも熱ゾーン間での温度センサーの共有をサポートします。

MTL の詳細については、"温度管理の Windows"をという名前のドキュメントを参照してください、 [Microsoft Connect web サイト](https://aka.ms/connect-redirect?DownloadID=48106)します。

これらの機能を使用する Oem は次のデバイスに固有のメソッドを含めることができます (\_DSM)、温度のゾーンの名前空間。

## <a name="function-1-minimum-throttle-limit"></a>関数 1:最小のスロットルの制限


\_熱の最小のスロットルの制限の DSM コントロール メソッドのパラメーターは次のようにします。

### <a name="arguments"></a>引数

-   **Arg0:** UUID = 14d399cd-7a27-4b18-8fb4-7cb7b9f4e500
-   **Arg1:** リビジョン ID = 0
-   **Arg2:** 関数インデックス = 1
-   **Arg3:** 空のパッケージ (未使用)

### <a name="return"></a>戻り値

現在の最小のスロットルの制限を表す整数値は、割合として表されます。 Windows では、この値を下回るスロットル制限は設定されません。
## <a name="function-2-temperature-sensor-device"></a>関数 2:温度センサー デバイス


\_温度センサーのデバイスの DSM コントロール メソッドのパラメーターは次のようにします。

### <a name="arguments"></a>引数

-   **Arg0:** UUID = 14d399cd-7a27-4b18-8fb4-7cb7b9f4e500
-   **Arg1:** リビジョン ID = 0
-   **Arg2:** 関数インデックス = 2
-   **Arg3:** 空のパッケージ (未使用)

### <a name="return"></a>戻り値

この温度のゾーンの温度を返すデバイスへの参照。
## <a name="temperature-sensor-device-dependency-requirement"></a>温度センサー デバイス依存関係の要件


温度センサー デバイス経由で報告された場合は\_DSM 関数インデックス 2、熱のゾーンがさらに、使用する必要を\_温度センサーのデバイスの温度のゾーンの依存を識別する DEP オブジェクト。

**注**  関数インデックス 0 の各\_DSM がサポートされている関数のインデックスのセットを返しますは常に必要とするクエリ関数を示します。 詳細については、セクション 9.14.1 を参照してください。"\_DSM (デバイスの特定のメソッド)"、ACPI 5.0 仕様の。

 

 

 




