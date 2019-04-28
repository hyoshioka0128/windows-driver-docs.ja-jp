---
title: プラグ アンド プレイ SCSI ミニポート ドライバーのレジストリ エントリ
description: プラグ アンド プレイ SCSI ミニポート ドライバーのレジストリ エントリ
ms.assetid: d4c7c8ee-9d04-4fd4-9b70-2630d2ce6401
keywords:
- SCSI ミニポート ドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- プラグ アンド プレイ WDK SCSI
- PnPInterface
- レジストリ WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03afdab59d1a54b7d24f137405ffc2b1785e4ac9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366245"
---
# <a name="registry-entries-for-plug-and-play-scsi-miniport-drivers"></a>プラグ アンド プレイ SCSI ミニポート ドライバーのレジストリ エントリ


## <span id="ddk_registry_entries_for_plug_and_play_scsi_miniport_drivers_kg"></span><span id="DDK_REGISTRY_ENTRIES_FOR_PLUG_AND_PLAY_SCSI_MINIPORT_DRIVERS_KG"></span>


プラグ アンド プレイをサポートするために、SCSI ミニポート ドライバーが必要です。

-   HBA のサービスとしてインストールします。

-   **PnPInterface**インターフェイスを示すレジストリ エントリで、ミニポート ドライバーがプラグ アンド プレイをサポートします。

SCSI HBA のサービスとしてのミニポート ドライバーのインストールは、そのデバイスを制御するための適切なドライバーを指定された HBA のプラグ アンド プレイ ハードウェア ID と一致するセットアップ情報 (INF) ファイルを提供することで通常行われます。 詳細については、INF ファイルの設定は、次を参照してください。[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)*します。*

HBA、用のサービスとしてのミニポート ドライバーがインストールされていない場合、 **PnPInterface**レジストリ エントリは*ように*ミニポート ドライバーを初期化します。 指定したインターフェイスは、プラグ アンド プレイ適切な HBA を検索する場合にのみ初期化されます。 サービスが正しく割り当てられていない場合、HBA に、プラグ アンド プレイはしないデバイスを検出したときに通知するドライバーを決定します。 この動作は仕様であり、ミニポート ドライバーはこれを回避しようとはしないでください。

**PnPInterface**の下にレジストリ エントリを作成する必要があります、**サービス**ミニポート ドライバーのキー。 たとえば、次のレジストリ エントリは、近づけという架空のミニポート ドライバーのプラグ アンド プレイを使用できます。

```cpp
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services
    \Twiddle
        \Parameters
            \PnpInterface
                5 : REG_DWORD : 1
                1 : REG_DWORD : 1
                2 : REG_DWORD : 1
                8 : REG_DWORD : 1
```

REG を前の値\_インターフェイスに対応して DWORD\_型で宣言された型の列挙*miniport.h*します。 この例の値を示します近づけ、ミニポート ドライバーが、次のインターフェイスのプラグ アンド プレイをサポートしています。**PCIBus** (5) **Isa** (1) **Eisa** (2) と**PCMCIABus** (8)。 次のレジストリ値\_DWORD がインターフェイスのプラグ アンド プレイのサポートを示すフラグ。 (現時点では、このフラグの値を指定できますが、存在する必要があります。 今後、フラグあります省略可能)。

後に、 **PnPInterface**値は、レジストリで設定し、システムの再起動、ミニポート ドライバーがプラグ アンド プレイ ドライバーとして初期化することができます。 SCSI ポート ドライバーでは初期化中に、ミニポート ドライバーがプラグ アンド プレイまたはレガシ ドライバーとして実行するかどうかを確認するレジストリを確認します。 SCSI ポート ドライバーは、(たとえば、PCI、ISA など)、ミニポート ドライバーをサポートするインターフェイスの種類ごとにレジストリを確認します。 これは、複数インタ フェース ミニポート ドライバーのライターのデバッグを簡略化するには、主にものです。 ミニポート ドライバー開発者は、ミニポート ドライバーがすべてのプラグ アンド プレイ ドライバー インターフェイスは、ドライバーとして実行されていることができることを確認してくださいをサポートしています。

 

 




