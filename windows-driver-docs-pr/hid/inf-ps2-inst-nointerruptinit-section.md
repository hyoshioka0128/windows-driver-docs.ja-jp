---
title: INF PS2_Inst.NoInterruptInit セクション
description: INF PS2_Inst.NoInterruptInit セクション
ms.assetid: e84cc7fc-8b17-4119-84f9-12ac888c68aa
keywords:
- INF ファイル WDK 非 HID キーボード/マウス
- PS2_Inst.NoInterruptInit セクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d699a4005cd977665b74bb4eb293ecf337548bb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364680"
---
# <a name="inf-ps2instnointerruptinit-section"></a>INF PS2\_Inst.NoInterruptInit セクション





**\[PS2\_Inst.NoInterruptInit\]**
**AddReg** = <em>追加 reg セクション</em>**します。AddReg**マウス クラスのインストーラーが場合に、このセクションでは、ディレクティブを実行、*を無効にする*内のエントリを[INF **PS2\_Inst.NoInterruptInit.Bios**セクション](inf-ps2-inst-nointerruptinit-bioses-section.md)システム BIOS のバージョンと一致します。

### <a name="entries-and-values"></a>エントリと値

<a href="" id="add-reg-section"></a>*追加 reg セクション*  
指定します、 **AddReg**マウス クラスのインストーラーを使用して、デバイスのハードウェア キーのレジストリ値を設定する」セクション。 レジストリ値では、システムが割り込みを使用して、またはポーリングによってマウス デバイスを初期化するかどうかを決定します。

### <a href="" id="comments"></a>「解説」

このセクションでと組み合わせて使用のみを[INF **PS2\_Inst.NoInterruptInit.Bioses**セクション](inf-ps2-inst-nointerruptinit-bioses-section.md)します。 このセクションの主な目的は、指定する、 **AddReg**マウス デバイスのハードウェア キーにレジストリ値を追加するセクション。

### <a name="add-reg-section-entries"></a>*追加 reg セクション エントリ*

**HKR**、および"**DisableInitializePolledUI**"、0x00010001, 1 **HKR**、および"**MouseInitializePolled**"、0x00010001、1

<a href="" id="disableinitializepolledui"></a>**DisableInitializePolledUI**  
21 を指定します\_DWORD フラグを示すかどうか、**高速初期化**プロパティ ページでチェック ボックスが表示されます。 場合**DisableInitializePolledUI**が 0 以外の値に設定すると、チェック ボックスは使用できません。 それ以外の場合、チェック ボックスは使用できます。

<a href="" id="mouseinitializedpolled"></a>**MouseInitializedPolled**  
21 を指定します\_システムがそれを初期化するためにデバイスをポーリングする必要があるかどうかを示す DWORD フラグ。 場合**MouseInitializedPolled**設定は、1 つに、システムはマウス デバイスをポーリングは、それ以外の場合、システムが割り込みを使用します。

 

 




