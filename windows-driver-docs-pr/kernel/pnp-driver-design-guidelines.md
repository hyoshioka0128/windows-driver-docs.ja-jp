---
title: PnP ドライバー設計のガイドライン
description: PnP ドライバー設計のガイドライン
ms.assetid: 4e4a6a8e-3c7f-4561-bbe1-a8c06fe22d0a
keywords:
- PnP WDK カーネルでは、デザインのガイドライン
- プラグ アンド プレイ WDK カーネルでは、デザインのガイドライン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 368f95f7c62af38a3bcd99033c160b66cffb1382
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549235"
---
# <a name="pnp-driver-design-guidelines"></a>PnP ドライバー設計のガイドライン





プラグ アンド プレイを提供します。

-   インストールされているハードウェアの動的自動検出

-   ハードウェア リソースの割り当て (および再割り当て)

-   適切なドライバーの読み込み

-   ドライバー、PnP システムと対話するためのインターフェイス

-   ドライバーとアプリケーションについては、ハードウェア環境での変更のためのメカニズム

PnP をサポートするには、ドライバーは次のガイドラインに従う必要があります。

-   含める必要があります、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchpnp-routines#feedback)ルーチン。

    このディスパッチ ルーチンを処理する必要があります[ **IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)要求と関連付けられているマイナー機能コード。 詳細については、次を参照してください。 [DispatchPnP ルーチン](dispatchpnp-routines.md)します。

-   ハードウェアは、検索する必要があります。

    PnP マネージャーが、ハードウェア デバイスの存在を判断します。 呼び出すことによって、ドライバーに通知 PnP マネージャーでは、デバイスを検出すると、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。 システムを起動すると、またはいつでも、ユーザーは、デバイスを追加するか、実行中のシステムから削除しますと、ハードウェアを検出できます。

-   ハードウェア リソースいない割り当てる必要があります。

    PnP ドライバーでは、デバイスで使用する可能性のあるリソースの一覧で、PnP マネージャーを提供する必要があります。 PnP マネージャーは、デバイスごとにリソースを割り当てると、各デバイスの割り当てのドライバーへの通知を送信するとき、 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。 ドライバーは、したがってハードウェア リソースのさまざまな構成の操作の対応である必要があります。

一部のドライバーは、PnP の詳細とシステム提供ポートまたはクラス ドライバーによる電源管理から分離します。 たとえば、SCSI ポート ドライバー影響を受けないように SCSI ミニポート ドライバー、PnP システム、電源の詳細の多くのので SCSI ミニポート ドライバーは電源と PnP Irp を直接処理する必要はありません。 このようなドライバー、PnP 必要なサポートの詳細については、ドライバー固有のドキュメントを参照してください。

 

 




