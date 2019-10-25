---
title: PnP ドライバーの設計ガイドライン
description: PnP ドライバーの設計ガイドライン
ms.assetid: 4e4a6a8e-3c7f-4561-bbe1-a8c06fe22d0a
keywords:
- PnP WDK カーネル、設計ガイドライン
- WDK カーネルのプラグアンドプレイ設計ガイドライン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29ab13bb1d2e1802fcaab057b8c20f04c6f3b200
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838507"
---
# <a name="pnp-driver-design-guidelines"></a>PnP ドライバーの設計ガイドライン





プラグアンドプレイは次のとおりです。

-   インストールされているハードウェアの自動および動的な認識

-   ハードウェアリソースの割り当て (および再割り当て)

-   適切なドライバーの読み込み

-   PnP システムと対話するドライバーのインターフェイス

-   ハードウェア環境の変更について学習するためのドライバーとアプリケーションのメカニズム

PnP をサポートするには、ドライバーは次のガイドラインに従う必要があります。

-   [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchpnp-routines#feedback)ルーチンが含まれている必要があります。

    このディスパッチルーチンでは、 [**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)要求と関連するマイナー関数コードを処理する必要があります。 詳細については、「 [DispatchPnP ルーチン](dispatchpnp-routines.md)」を参照してください。

-   ハードウェアを検索することはできません。

    PnP マネージャーは、ハードウェアデバイスの有無を判断する役割を担います。 PnP マネージャーは、デバイスを検出すると、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出してドライバーに通知します。 システムが起動したとき、またはユーザーが実行中のシステムからデバイスを追加または削除したときに、ハードウェアを検出できます。

-   ハードウェアリソースを割り当てることはできません。

    PnP ドライバーは、デバイスが使用する可能性のあるリソースのリストを PnP マネージャーに提供する必要があります。 PnP マネージャーは、各デバイスにリソースを割り当て、 [ **\_デバイス要求の開始\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)が送信されたときに、各デバイスの割り当てをドライバーに通知します。 そのため、ドライバーは、ハードウェアリソースのさまざまな構成を使用できる必要があります。

一部のドライバーは、システムによって提供されるポートまたはクラスドライバーによって、PnP および電源管理の詳細から分離されています。 たとえば、scsi ポートドライバーは SCSI ミニポートドライバーを電源および PnP システムの多くの詳細から分離するので、SCSI ミニポートドライバーは、電源と PnP の Irp を直接処理する必要がありません。 このようなドライバーについては、ドライバー固有のドキュメントを参照して、必要な PnP サポートの詳細を確認してください。

 

 




