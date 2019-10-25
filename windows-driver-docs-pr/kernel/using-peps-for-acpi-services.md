---
title: ACPI サービス用 PEP の使用
description: このトピックでは、ACPI サービス用のプラットフォーム拡張機能プラグイン (PEPs) の使用について説明します。
ms.assetid: 80ED3B80-A1FF-4A41-BA88-EC1C832C4639
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5a42590abc050b137b6db68e2516e0061e45e0b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835882"
---
# <a name="using-peps-for-acpi-services"></a>ACPI サービス用 PEP の使用


このトピックでは、ACPI サービス用のプラットフォーム拡張機能プラグイン (PEPs) の使用について説明します。

PEPs は、動的なランタイム ACPI メソッドを提供します。 静的テーブル (FADT、MADT、DBG2 など) は、ACPI ファームウェア、および DSDT/SSDT デバイス階層に実装する必要があります。

PEPs は、SoC 以外の電源管理方法に使用することを目的としています。 インストール可能なバイナリであるため、ファームウェアフラッシュを必要とする ACPI ファームウェアではなく、その場で更新できます。 つまり、Windows Update に更新されたドライバーを投稿することによって、既に出荷されているプラットフォームの電源管理コードを改善することができます。 電源管理は PEPs の本来の目的でしたが、任意の ACPI ランタイムメソッドを提供または上書きするために使用できます。

PEPs play は、名前空間階層をファームウェア DSDT に指定する必要があるため、ACPI 名前空間階層構造の構築ではロールがありません。 ACPI ドライバーは、実行時にメソッドを評価するときに、対象のデバイスに対して PEP の実装されたメソッドを確認し、存在する場合は PEP を実行してファームウェアのバージョンを無視します。 ただし、デバイス自体はファームウェアで定義されている必要があります。

PEPs を使用して電源管理を提供することは、使用可能なツールにより、ACPI ファームウェア用に記述されたコードよりもはるかに簡単にデバッグできます。 ACPI ファームウェアをデバッグするためのツールは、ほとんどの場合、ツールオプションは限られています。 これに対して、PEPs は Windows ドライバーとして開発されるため、開発者は最も使いやすい開発ツールやデバッグツールを使用できます。

ACPI サービスの代わりに PEP を使用する場合、サービスの役割を要求するために特別な操作や操作は必要ありません。 PEP にメソッドが実装されている場合、Windows はそれを自動的に使用します。 同じデバイス上の同じメソッドのファームウェアバージョンが指定されている場合、そのバージョンは無視されます。

PEPs は、デバイスドライバーでサービスを利用できるようにするために事前に読み込まれています。 さらに、Windows を通じた抽象化レイヤーは、デバイスドライバーに対して透過的になるように設計されています。 PEP が使用されていないかのように、ドライバーは ACPI メソッドと対話できることを期待します。

デバイス電源管理 (DPM) と ACPI サービスの両方に PEP を使用する場合は、個別の PEP ハンドルを使用することをお勧めしますが、これは単なる優先事項にすぎません。 ハンドルを共有する場合、デバイスのハンドルは同じであるため、DPM と ACPI 状態を簡単に追跡できます。 ただし、処理の有効期間の管理は少し複雑になります。 PEP は、そのハンドルに対して DPM と ACPI の両方のサービスが破棄された後にのみ削除されることを確認するために、ハンドルの参照カウントを提供する必要があります (つまり、 [**pep\_dpm\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)と\_PEP の登録を解除します。 [ **\_ACPI\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)がそのハンドルで受信されたことを知らせる) に通知します。 異なるハンドルを使用すると、DPM と ACPI の状態が別々に追跡されますが、有効期間の管理はより簡単になります。 この場合、対応する登録解除通知が送信されると、ハンドルが破棄される可能性があります。

ACPI リソースを操作するプロセスを簡略化するために、電源管理フレームワーク (PoFx) は PEP\_要求\_COMMON\_ACPI\_\_を\_BIOS\_リソースヘルパールーチンに変換して、ACPI に変換します。BIOS リソースに対するリソース。

PEPs は、PoFx からの ACPI 通知に応答して同期的に実行できない作業のスケジュールを担当しますが、使用される方法は PEP 開発者によって決定されます。 通常、PEP は、一部の内部キューで作業をキューに入れ、必要に応じてワーカースレッドを開始します。 また、作業が一部の外部イベント (デバイスの割り込みなど) を待機する必要があり、そのイベントのコンテキストで処理される可能性もあります。 処理が完了すると、PEP は、 [**pep\_カーネル\_情報\_構造体\_V3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_kernel_information_struct_v3)-&gt;[*requestworker*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pofxcallbackrequestworker)() を呼び出すことによって、操作を照会するように pofx を要求できます。 これに対して、PoFx は、dpm 通知ハンドラー ([*AcceptDeviceNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifydpm)) または[**pep\_通知\_ACPI\_work 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を実装する PEPs に対して、 [**pep\_\_dpm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を送信します。ACPI 専用の通知ハンドラー ([*AcceptAcpiNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifyacpi)) を実装する PEPs。

## <a name="related-topics"></a>関連トピック
[ACPI システムの説明テーブル](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-system-description-tables)  
[**PEP\_DPM\_\_デバイスの登録を解除します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[**PEP\_\_ACPI\_\_デバイスの登録解除を通知する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[**PEP\_カーネル\_情報\_STRUCT\_V3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/ns-pepfx-_pep_kernel_information_struct_v3)  
[**PEP\_DPM\_WORK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[**PEP\_\_ACPI\_WORK に通知します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[*RequestWorker*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pofxcallbackrequestworker)  
[*AcceptDeviceNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifydpm)  
[ACPI 通知](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  



