---
title: バッテリーのデバイス固有のメソッド
description: このトピックでは、_DSM control メソッドとパッシブの熱バッテリ管理用のパラメーターについて説明します。
ms.assetid: 622803F4-2548-4E8A-A330-179ABDF374AD
ms.date: 05/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5d31df93181b72a9c42767fe2e494ea5c5a8962e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328104"
---
# <a name="battery-device-specific-method"></a>バッテリーのデバイス固有のメソッド


Microsoft の定義、プラットフォームによって、バッテリのパッシブの温度管理をサポートするために、\_熱の調整、プラットフォーム ファームウェアとの通信に DSM メソッドが、バッテリの熱のゾーンでセットを制限します。

詳細については、次を参照してください。、**熱ゾーン**セクション、 [ACPI には、デバイスが定義されている](acpi-defined-devices.md#thermal)トピック。

## <a name="function-1-battery-thermal-limit"></a>関数 1:バッテリ温度の上限


\_バッテリの充電熱制限関数の DSM 制御メソッドのパラメーターは、次のようにします。

### <a name="arguments"></a>引数

-   **Arg0:** UUID = 4c2067e3-887d-475c-9720-4af1d3ed602e
-   **Arg1:** リビジョン = 0
-   **Arg2:** 関数インデックス = 1
-   **Arg3:** 温度の上限 (整数 0 ~ 100 の値)

### <a name="return"></a>戻り値

なし。 ファームウェアが充電魅力的なときに、現在の温度の上限を考慮して責任を負います。
 

 




