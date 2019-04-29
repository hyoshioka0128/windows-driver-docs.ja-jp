---
title: powertriage
description: システムとデバイスの電源に関する powertriage 拡張機能が表示されます概要情報に関連するコンポーネント。
ms.assetid: A202ED64-B706-42AC-B058-C44321C9171F
keywords:
- Windows デバッグ powertriage
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- powertriage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 90a760ab85eb0a5ea9b484754eb987dbd2c2a7da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334370"
---
# <a name="powertriage"></a>!powertriage


! Powertriage 拡張機能、システムに関する概要情報を表示してデバイスの電源関連のコンポーネント。 追加情報を収集するために使用できる関連するコマンドへのリンクも提供します。 ! Powertriage コマンドにパラメーターがありません。 このコマンドは、ライブのカーネル モードのデバッグの両方と、クラッシュ ダンプ ファイルの分析のために使用できます。

構文

```dbgcmd
!powertriage
```

## <a name="span-idddkthreaddbgspanspan-idddkthreaddbgspanparameters"></a><span id="ddk__thread_dbg"></span><span id="DDK__THREAD_DBG"></span>パラメーター


なし

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 10 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

! Powertriage 拡張機能には、次の情報が表示されます。

1. 電源の状態と共に、[デバイス] ノードの! podev デバイスのすべてのオブジェクト。
2. リンク[ **! rcdrkd.rcdrlogdump** ](-rcdrkd-rcdrlogdump.md)ドライバーが、IFR を有効にした場合。 IFR の詳細については、次を参照してください。[を使用して転送トレース レコーダー (IFR) KMDF および UMDF 2 ドライバー](https://msdn.microsoft.com/library/windows/hardware/dn940485)します。
3. リンク[ **! wdfkd.wdfdriverinfo** ](-wdfkd-wdfdriverinfo.md)と[ **! wdfkd.wdflogdump** ](-wdfkd-wdflogdump.md) WDF ドライバー。
4. リンクします。 fxdevice PoFx デバイス。 PoFX の詳細については、次を参照してください。 [、電源管理フレームワークの概要](https://msdn.microsoft.com/library/windows/hardware/hh406637)します。
出力例を次に示します、! powertriage コマンド。

```dbgcmd
kd> !powertriage

System Capabilities :
  Machine is not AOAC capable.

Power Capabilities:
PopCapabilities @ 0xfffff8022f6c4380
  Misc Supported Features:  PwrButton S1 S3 S4 S5 HiberFile FullWake
  Processor Features:      
  Disk Features:           
  Battery Features:        
  Wake Caps
    Ac OnLine Wake:         Sx
    Soft Lid Wake:          Sx
    RTC Wake:               S4
    Min Device Wake:        Sx
    Default Wake:           Sx



Power Action:

PopAction :fffff8022f6ba550
    Current System State..: Working
    Target System State...: Unspecified
    State.................: - Idle(0)

Devices with allocated Power IRPs:

    +  ACPI\PNP0C0C\2&daba3ff&1
       0xffffe00023939ad0 ACPI D0 !podev  WAIT_WAKE_IRP !irp Related Threads 

    +  USB\ROOT_HUB30\5&2c60645a&0&0
       0xffffe0002440ac40 USBXHCI D2 !podev  WAIT_WAKE_IRP !irp Related Threads !rcdrlogdump !wdfdriverinfo !wdflogdump 
         Upper DO 0xffffe00024415a10 USBHUB3 !podev 


    +  USB\ROOT_HUB30\5&d91dce5&0&0
       0xffffe00023ed4d30 USBXHCI D2 !podev  WAIT_WAKE_IRP !irp Related Threads !rcdrlogdump !wdfdriverinfo !wdflogdump 
         Upper DO 0xffffe000249d8040 USBHUB3 !podev 

    +  PCI\VEN_8086&DEV_27E2&SUBSYS_01DE1028&REV_01\3&172e68dd&0&E5
       0xffffe000239e5880 pci D0 !podev FxDevice: !fxdevice  WAIT_WAKE_IRP !irp Related Threads 
         Upper DO 0xffffe000239c0e50 ACPI !podev 
           Upper DO 0xffffe000239f7040 pci !podev 


    +  PCI\VEN_14E4&DEV_167A&SUBSYS_01DE1028&REV_02\4&24ac2e11&0&00E5
       0xffffe000231e6060 pci D0 !podev  WAIT_WAKE_IRP !irp Related Threads 
         Upper DO 0xffffe00024359050 b57nd60a !podev 


Device Tree Info: 

    !devpowerstate

    !devpowerstate Complete


Links:
!poaction
!cstriage
!pdctriage
!pdcclients
!fxdevice
!pnptriage
```

**ダンプ ファイル電源障害の分析**

! Powertriage 拡張機能は、不適切な電源状態の情報に関連するシステムのクラッシュを調べることに役立ちます。 たとえばの場合[ **0x9F のバグ チェック。ドライバー\_POWER\_状態\_エラー**](bug-check-0x9f--driver-power-state-failure.md)、拡張機能は、すべての割り当てられた電源 Irp、と共に関連するデバイス スタックを表示します。

1. リンク、 [ **! irp** ](-irp.md)関連 Irp のコマンド。
2. リンク、 [ **! findthreads** ](-findthreads.md)コマンド関連の IRP にします。 以降より高い相関、検索条件のスレッドをスレッドが最初に一覧表示を表示、検索条件の一部として、IRP が追加されます。
ある Irp がデバッグに役立つ機能のすべてのデバイス スタックをダンプするケース! 分析、クラッシュに関連付けられている IRP を正しく識別することができます。

 

 





