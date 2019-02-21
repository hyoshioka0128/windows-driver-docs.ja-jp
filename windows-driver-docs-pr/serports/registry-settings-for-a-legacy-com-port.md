---
title: 従来の COM ポートのレジストリ設定
description: 従来の COM ポートのレジストリ設定
ms.assetid: 043ac1f5-eeb1-4828-8417-b3c6d76b4322
keywords:
- シリアル ドライバー WDK では、COM ポート
- COM ポートの WDK シリアル デバイス
- COM ポート、シリアル デバイス WDK
- 従来の COM ポートの WDK シリアル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f74c82f59edc994e65027b175553c367e064af8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560643"
---
# <a name="registry-settings-for-a-legacy-com-port"></a>従来の COM ポートのレジストリ設定





このトピックでは、シリアルがレガシを使用しているレジストリ設定を説明します[COM ポート](configuration-of-com-ports.md)します。 シリアルは、常に COM ポートとしてレガシ シリアル デバイスを構成します。

シリアルは、従来の COM ポートを列挙したときに、これらのエントリの値を照会します。 デバイスに固有のエントリの値が存在しない場合、シリアルはシリアル サービス値を使用します。

従来の COM ポートのレジストリ設定が下にある対応するレガシ COM ポート サブキーの下には、 **.\\サービス\\シリアル\\パラメーター**キー。

次のエントリの値が同じの説明に従って、[プラグ アンド プレイ シリアル デバイス](registry-settings-for-a-plug-and-play-serial-device.md):

-   **ClockRate**

-   **PortIndex**

-   **インデックスを作成**

-   **RxFIFO**

-   **TxFIFO**

-   **MaskInverted**

-   **DisablePort**

-   **ForceFifoEnable**

次の追加エントリの値は、従来の COM ポートと共に使用されます。

<a href="" id="portaddress--reg-dword-"></a>**PortAddress** (REG\_DWORD)  
COM ポートの制御レジスタの無変換の基本 I/O アドレスを指定します。 シリアルでは、この値を読み取ります。 値 0 にすることはできません。 既定値**PortAddress** 0x00000000 します。

<a href="" id="interrupt--reg-dword-"></a>**割り込み**(REG\_DWORD)  
バスの種類に応じて、無変換割り込みベクトルを指定します。 シリアルでは、この値を読み取ります。 値 0 にすることはできません。 既定値**Interrupt** 0x00000000 します。

<a href="" id="dosdevices--reg-sz-"></a>**\Dosdevices\z** (REG\_SZ)  
COM ポートの名前を指定します。 通常、COM での COM ポートの名前は<em>&lt;n&gt;、</em>場所&lt; *n&gt;*  COM ポートの番号からインストーラーを取得するには、 [COM ポート データベース](com-port-database.md)します。 ただし、COM ポートの名前に設定できますいずれ以外**NULL**文字列。 シリアルでは、ポート名を使用して、ユーザー モードで表示されている COM ポートへのシンボリック リンクを作成します。 既定値**\dosdevices\z**は、 **NULL**文字列。

<a href="" id="interruptstatus--reg-dword-"></a>**InterruptStatus** (REG\_DWORD)  
割り込み状態のレジスタの生の I/O のアドレスを指定します。 シリアルでは、この値を読み取ります。 ポートがスタンドアロンのポートの場合、値は省略されます。 マルチポートのデバイス上のポートがの場合、値は 0 にすることはできません。 既定値**InterruptStatus** 0x00000000 します。

<a href="" id="busnumber--reg-dword-"></a>**BusNumber** (REG\_DWORD)  
バスの種類のシステム全体のバス番号を指定します。 シリアルでは、この値を読み取ります。 既定値**BusNumber** 0x00000000 します。

<a href="" id="bustype--reg-dword-"></a>**BusType** (REG\_DWORD)  
バスの種類を指定します。 シリアルでは、この値を読み取ります。 既定値**BusType**ドライバーの初期化中にシリアルによって決定されます。

<a href="" id="interruptmode--reg-dword-"></a>**InterruptMode** (REG\_DWORD)  
割り込みモードを指定します。 シリアルでは、この値を読み取ります。 既定値**InterruptMode** cm\_リソース\_INTERRUPT\_LATCHED します。

<a href="" id="interruptlevel--reg-dword-"></a>**InterruptLevel** (REG\_DWORD)  
バスの種類に適した生の割り込みのレベルの値を指定します。 シリアルでは、この値を読み取ります。 既定値**InterruptLevel** 0x00000000 します。

<a href="" id="pnpdeviceid--reg-sz-"></a>**PnPDeviceID** (REG\_SZ)  
プラグ アンド プレイ デバイスのプラグ アンド プレイ デバイスの識別子を指定します。 シリアルでは、この値を読み取ります。 既定値**PnPDeviceID**は、 **NULL**文字列。

<a href="" id="legacydiscovered--reg-dword-"></a>**LegacyDiscovered** (REG\_DWORD)  
シリアルが、プラグ アンド プレイ manager がデバイスを報告したかどうかを示すブール フラグです。 シリアルを読み込んでこの値を設定します。 場合**LegacyDiscovered**が 0 以外の場合、シリアルが以前デバイスを報告しました、もう一度デバイスを報告しません。 それ以外の場合、シリアル デバイスを報告および 0x00000001 にエントリの値を設定します。

 

 




