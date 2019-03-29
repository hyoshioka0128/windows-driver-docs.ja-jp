---
title: Windows ボタン配列のデバイス固有のメソッド (_DSM)
description: Windows のボタン ユーザー インターフェイス (UI) の進化をサポートするためには、Windows は、この記事では、特定のデバイス メソッド (_DSM) 説明されている関数を使用した Windows ボタン配列のデバイスを定義します。
ms.assetid: B79ED0F9-B46A-4915-8FF3-5CF3D2E0E945
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fdfa6c35d0cfc715401c7b89f42f6c9c35d8466
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572966"
---
# <a name="windows-button-array-device-specific-method-dsm"></a>Windows ボタン配列デバイス固有のメソッド (\_DSM)


Windows を Windows のボタン ユーザー インターフェイス (UI) の進化をサポートするには、デバイス固有のメソッドを定義します (\_DSM) この記事で説明されている関数を使用した Windows ボタン配列デバイス。

## <a name="function-1-power-button-properties"></a>関数 1:電源ボタンのプロパティ


\_電源ボタンのプロパティ関数の DSM コントロール メソッドのパラメーターは次のようにします。

### <a name="arguments"></a>引数

-   **Arg0:** UUID = dfbcf3c5-e7a5-44e6-9c1f-29c76f6e059c
-   **Arg1:** リビジョン ID = 0
-   **Arg2:** 関数インデックス = 1
-   **Arg3:** 空のパッケージ (未使用)

### <a name="return"></a>戻り値

次のビット フィールドの定義を含む整数 (DWORD):

-   ビット 31 に 33:予約済み (0 にする必要があります)。
-   ビット 2:[電源] ボタンが構成されている両方のキーを押してを検出し、リリース イベント、およびオペレーティング システムにこれらのイベントを報告する場合、このビットを 1 に設定する必要があります。 それ以外の場合、このビットは 0 にする必要があります。
-   ビット 1:このビットは割り込みコント ローラーに電力 ボタンがワイヤード (有線) の場合、1 に設定する必要があります (GPIO またはそれ以外の場合) レベルの検出をサポートします。 それ以外の場合、このビットは 0 にする必要があります。
-   ビット 0:プラットフォームは、10 秒以上に時間を ACPI 電源ボタンのオーバーライドをサポートしている場合、このビットを 1 に設定する必要があります。 それ以外の場合、このビットは 0 にする必要があります。

**注**  関数インデックス 0 の各\_DSM がサポートされている関数のインデックスのセットを返しますは常に必要とするクエリ関数を示します。 詳細については、セクション 9.14.1 を参照してください。"\_DSM (デバイスの特定のメソッド)"で、 [ACPI 5.0 仕様](https://www.uefi.org/specifications)します。

 

 

 




