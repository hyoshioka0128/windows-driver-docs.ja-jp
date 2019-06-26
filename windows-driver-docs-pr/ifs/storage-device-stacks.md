---
title: ストレージ デバイス スタック
description: ストレージ デバイス スタック
ms.assetid: dc2c532d-4ec6-4c97-bb94-429dd06f7b7c
keywords:
- フィルター ドライバー WDK ファイル システム、記憶域デバイス スタック
- ファイル システム フィルター ドライバー WDK、記憶域デバイス スタック
- 記憶域デバイス スタック WDK ファイル システム
- デバイス履歴の WDK ファイル システム
- デバイス ツリー WDK ファイル システム
- PnP デバイス ツリー WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c02b4324a3ed0fc0c25666fe0c9ed06e11ce2000
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371315"
---
# <a name="storage-device-stacks"></a>ストレージ デバイス スタック


## <span id="ddk_storage_device_stacks_if"></span><span id="DDK_STORAGE_DEVICE_STACKS_IF"></span>


ほとんどの記憶装置ドライバーは、PnP デバイス ドライバーが読み込まれ、PnP マネージャーによって管理されます。 記憶装置が、PnP で表される*デバイス ツリー*、[デバイス] ノードを含むまたは*devnode*マシン上のすべての論理または物理デバイスにします。 ファイル システムとファイル システム フィルター ドライバーがないこと PnP デバイス ドライバーに注意してください。したがって、PnP デバイス ツリーにはそれらの devnode を含まれません。 PnP デバイス ツリーに関する詳細については、次を参照してください。[デバイス ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)します。

特定の記憶域デバイスの devnode が含まれています、*記憶域デバイス スタック*; デバイスのデバイスの記憶装置デバイス ドライバーを表すオブジェクトを接続しているデバイスのチェーンになります。 ディスクなどの記憶域デバイスには、(パーティションまたはダイナミック ボリューム) 1 つまたは複数の論理ボリュームが含まれている可能性があります、ため、記憶域デバイス スタック自体スタックよりも、ツリーのようにより多くの場合は。 このツリーのルートには、記憶域アダプターまたは記憶域スタックと統合されている別のデバイス スタックの機能のデバイス オブジェクト (FDO) です。 このツリーのリーフでは、記憶域ボリュームとも呼ばれる、論理ボリュームの物理デバイス オブジェクト (PDO)<em>、</em>ファイル システム ボリュームをマウントできます。

ダイアグラムといくつかの一般的な記憶域デバイス スタックの説明については、記憶域デバイスの設計ガイドの次のセクションを参照してください。

[SCSI HBA のデバイス オブジェクトの例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-a-scsi-hba)

[IEEE 1394 コント ローラーのデバイス オブジェクトの例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-an-ieee-1394-controller)

 

 




