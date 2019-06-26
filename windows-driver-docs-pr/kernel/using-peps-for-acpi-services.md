---
title: ACPI サービス用 PEP の使用
description: このトピックでは、ACPI サービスのプラットフォーム拡張機能プラグイン (Pep) の使用についての情報を提供します。
ms.assetid: 80ED3B80-A1FF-4A41-BA88-EC1C832C4639
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 907c720c1541ae9a256ec9da2051fad972c91ae3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381583"
---
# <a name="using-peps-for-acpi-services"></a>ACPI サービス用 PEP の使用


このトピックでは、ACPI サービスのプラットフォーム拡張機能プラグイン (Pep) の使用についての情報を提供します。

Pep では、ACPI メソッド動的、ランタイムを提供します。 あります/SSDT のデバイスの階層と同様に、ACPI ファームウェアで (FADT、MADT、DBG2 など) は、静的なテーブルを実装する必要があります。

Pep は SoC を電源管理の方法を使用するためのものです。 これらは、インストール可能なバイナリであるため更新 - その場でファームウェア flash が必要ですが、ACPI ファームウェアではなく使用できます。 つまり、Windows Update で更新されたドライバを投稿することで既に出荷しているプラットフォームで、電源管理のコードを改善できます。 電源管理が、Pep の本来の目的が、指定または任意の ACPI ランタイム メソッドをオーバーライドすることができます。

Pep 役割を果たしますありません ACPI 名前空間の階層の作成にします。 ファームウェア名前空間の階層を指定する必要がありますので。 ACPI ドライバーでは、実行時のメソッドを評価するときは、対象のデバイスの PEP の実装されたメソッドに対して確認し、存在する場合は、PEP を実行し、ファームウェアのバージョンを無視することは。 ただし、デバイス自体の場合は、ファームウェアで定義されている必要があります。

Pep を使用して電源管理を提供するデバッグするために使用できるツール、ACPI ファームウェアの記述されたコードよりもはるかに簡単に指定できます。 ACPI のファームウェアをデバッグするためのツールが最も慣れていないし、ツールのオプションは制限されています。 これに対し、Pep は、開発者が使用できる任意の開発とデバッグ ツールは、最も見慣れた Windows ドライバーとして開発されています。

ACPI サービスの代わりに、PEP を使用して、特別なアクションまたは操作は必要ありません、サービスの役割を要求するには。 PEP にメソッドを実装すると、ときに Windows は自動的にそれを使用します。 同じデバイス上の同じメソッドのファームウェアのバージョンが指定されている場合は無視されます。

Pep は、サービスがデバイス ドライバーを使用できるように非常に早い段階読み込まれます。 さらに、Windows によって抽象化レイヤーはデバイス ドライバーに対して透過的に設計されています。 ドライバーは、PEP が使用されていない場合と同様に、ACPI メソッドと対話することができるはずです。

PEP (DPM) デバイスの電源管理と ACPI サービスの両方を使用する場合は、個別の PEP ハンドルの使用をお勧めしますが、これは、好みの問題のみです。 ときにハンドル DPM と ACPI の状態を共有に追跡できる簡単にデバイス ハンドルが同じであるため。 ただし、ハンドルの有効期間管理は、少し複雑です。 PEP は確認を識別するハンドルに対する参照カウントが DPM と ACPI の両方のサービスが破損している場合は、後は削除のみを提供する必要があります (つまり、どちらも[ **PEP\_DPM\_UNREGISTER\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)と[ **PEP\_通知\_ACPI\_登録解除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)されています。受信したそのハンドル)。 別のハンドルを使用している場合は、DPM と ACPI の状態が、個別に追跡されますが、ハンドルの有効期間管理が簡単です。 この場合、ハンドルを破棄することができます、対応する登録解除と通知が送信されます。

電源管理フレームワーク (PoFx) を ACPI リソースの操作のプロセスを簡素化するには、PEP を提供します\_要求\_共通\_ACPI\_変換\_TO\_BIOS\_ACPI リソースを BIOS のリソースに変換するヘルパー ルーチンのリソース。

Pep は PoFx から ACPI 通知に応答で同期的に実行できない作業をスケジュールする責任を負いますが、使用する方法は、PEP の開発者によって決定されます。 通常、PEP はいくつかの内部キューでの作業をキューし、必要な場合は、ワーカー スレッドを開始します。 作業がいくつかの外部イベント (デバイスの割り込みなど) を待機する必要があることもできますし、そのイベントのコンテキストで処理されます。 PEP が呼び出すことによって、作業を照会する PoFx を要求できます、作業を完了すると、 [ **PEP\_カーネル\_情報\_構造体\_V3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/ns-pepfx-_pep_kernel_information_struct_v3) - &gt; [ *RequestWorker*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pofxcallbackrequestworker)()。 PoFx を送信する応答で、 [ **PEP\_DPM\_作業通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)の DPM の通知ハンドラーを実装している Pep ([ *AcceptDeviceNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pepcallbacknotifydpm)) または[ **PEP\_通知\_ACPI\_作業通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)の PEPs ですACPI 専用通知ハンドラーを実装する ([*AcceptAcpiNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pepcallbacknotifyacpi))。

## <a name="related-topics"></a>関連トピック
[説明の ACPI システム テーブル](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-system-description-tables)  
[**PEP\_DPM\_登録解除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[**PEP\_通知\_ACPI\_登録解除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[**PEP\_カーネル\_情報\_構造体\_V3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/ns-pepfx-_pep_kernel_information_struct_v3)  
[**PEP\_DPM\_作業**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[**PEP\_通知\_ACPI\_作業**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[*RequestWorker*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pofxcallbackrequestworker)  
[*AcceptDeviceNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pepfx/nc-pepfx-pepcallbacknotifydpm)  
[ACPI の通知](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  



