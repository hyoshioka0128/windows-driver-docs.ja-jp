---
title: GPIO コントローラーの要件チェック リスト
description: このトピックでは、ハードウェア、ファームウェア、および Windows に公開されている一般的な目的入出力 (GPIO) コント ローラー デバイスのソフトウェア要件をまとめたものです。
ms.assetid: 8097F391-ABF0-44A6-94D2-243AFBA3F984
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07b0b5f9818c99a5c3f28bc8f14a84e957415ac7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337587"
---
# <a name="gpio-controller-requirements-checklist"></a>GPIO コントローラーの要件チェック リスト


このトピックでは、ハードウェア、ファームウェア、および Windows に公開されている一般的な目的入出力 (GPIO) コント ローラー デバイスのソフトウェア要件をまとめたものです。

## <a name="gpio-controller-hardware-requirements"></a>GPIO コント ローラーのハードウェア要件


-   GPIO コント ローラーは、SoC (、SPB バスによって接続されていない) に統合されます。

    エミュレートされた ActiveBoth の信頼性が向上します。

-   レベル モード割り込みがサポートされています。

    エミュレートされた ActiveBoth と Debounce エミュレーションの両方の機能に必要です。

-   割り込み極性を高、低の両方がサポートされています。

    エミュレートされた ActiveBoth と Debounce エミュレーションの両方の機能に必要です。

-   割り込みの極性は、実行時に再下手順で指定できます。

    エミュレートされた ActiveBoth と Debounce エミュレーションの両方の機能に必要です。

## <a name="gpio-controller-firmware-requirements"></a>GPIO コント ローラーのファームウェア要件


-   GPIO コント ローラー \_CRS にはコント ローラーのすべてのピン留めする銀行のすべてのリソースが含まれています。
-   GPIO コント ローラー \_CRS リソース順序銀行とシステムの割り込みマッピングを提供します。
-   \_AEI メソッド、およびイベント メソッド (\_Exx、 \_Lxx または\_EVT)、すべての ACPI の GPIO 通知イベントが存在します。
-   GPIO コント ローラー \_ActiveBoth 割り込みは、コント ローラーに接続されている場合に含まれる DSM がアサートされるロジックのロジックではなく高低い。
-   実装\_REG メソッドごとに GPIO コント ローラーの場合は、GeneralPurposeIO OpRegions の使用を禁止し、 \_REG では、リージョンのハンドラーが使用できないことを示します。
-   Debounce タイムアウトには debouncing を必要とするすべての割り込みの GPIOInt リソース記述子が含まれます。

## <a name="gpio-controller-driver-requirements"></a>GPIO コント ローラーのドライバーの要件


-   GpioClx と GPIO コント ローラー ドライバー間のインターフェイスのバージョン 2 をサポートします。

    -   実装、 [*クライアント\_QueryEnabledInterrupts* ](https://msdn.microsoft.com/library/windows/hardware/dn265184)コールバック関数。 これは、大幅に割り込みストームを診断する際に支援します。
    -   場合、 **BankIdlePowerMgmtSupported**フラグに設定されて、 [**コント ローラー\_BASIC\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh439358) GPIO コント ローラーのドライバーを構成します。実装する必要があります、 [*クライアント\_SaveBankHardwareContext* ](https://msdn.microsoft.com/library/windows/hardware/hh439419)と[*クライアント\_RestoreBankHardwareContext*](https://msdn.microsoft.com/library/windows/hardware/hh439414)コールバック関数、およびこれらの関数する必要があります保存/復元銀行のコンテキストに適切にマスク/マスク解除されて、割り込みの状態などです。 割り込みは、この関数が呼び出された時点で切断する保証はありませんが、マスクされる保証されている場合、接続されていることに注意してください。
    -   場合、 **DeviceIdlePowerMgmtSupported**フラグに設定されて、**コント ローラー\_BASIC\_情報**構造、 [*クライアント\_StartController* ](https://msdn.microsoft.com/library/windows/hardware/hh439424)と[*クライアント\_StopController* ](https://msdn.microsoft.com/library/windows/hardware/hh439430)コールバック機能する必要がありますを保存/復元すべての銀行のコンテキスト割り込みのマスク/マスク解除されて状態が適切になど。 割り込みは、この関数が呼び出された時点で切断する保証はありませんが、マスクされる保証されている場合、接続されていることに注意してください。
-   設定、 **EmulateDebouncing**フラグ、**コント ローラー\_BASIC\_情報**構造体。 これは、静電気 (ボタン、プラグインするときなど) の対象デバイスの割り込みのノイズ電磁波耐性が大幅に向上します。
-   設定、 **EmulateActiveBoth**フラグ、**コント ローラー\_BASIC\_情報**構造体、および、実装、 [*クライアント\_ReconfigureInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/hh698243)コールバック関数。 これにより、ActiveBoth 割り込みの信頼性の高い境界の検出。

 

 




