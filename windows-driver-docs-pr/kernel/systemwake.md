---
title: SystemWake
description: SystemWake
ms.assetid: 77390637-bb92-4634-a407-9a409a8a8acd
keywords:
- SystemWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc0dd08b7d799465daaaa88f24f415b7e89b7c6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382963"
---
# <a name="systemwake"></a>SystemWake





**SystemWake**のメンバー [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)デバイスが、システムを wake 最低 (最小を利用した) システム電源の状態が含まれています、または**PowerSystemUnspecified**デバイスは、システムをスリープ解除できない場合。

バス ドライバーは、デバイスを列挙したときにこの値を設定します。 高度なドライバーは、パワー状態値を変更できますが、低電力状態に変更できません。 たとえば、バス ドライバー設定**SystemWake** S3 には、デバイス スタック サポート ウェイク アップ S2 からのみのドライバーをさらより高度なドライバーは、S2 に値を変更できます。 ドライバーが変更された場合**SystemWake**を変更する必要がありますも[ **DeviceWake**](devicewake.md)、次のセクションで説明するようにします。

ドライバーはほとんどデバイス スタックの下方の変更された値を伝達する必要があります。 変更より制限の厳しいデバイス機能を作成、ため、下位のドライバーに要求を処理できないものは表示されません。 前の例より高度なドライバーは、下位のドライバーにかかわらない、このような要求のために s2 の場合より低電力状態からシステムをスリープ解除するための要求を失敗します。 ただし場合、下位のドライバーは、すべての変更である必要があります、送信できる、PnP [ **IRP\_MN\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)の処理中に、独自デバイス スタックを[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)します。

両方、 **SystemWake**と**DeviceWake**メンバーは、0 以外の場合 (つまり、いない**PowerSystemUnspecified**)、後、デバイスとそのドライバーのサポート、ウェイク アップのこのシステムで。

非 ACPI のハードウェアでこのメンバー常に含まれます 0 (**PowerSystemUnspecified**)。

 

 




