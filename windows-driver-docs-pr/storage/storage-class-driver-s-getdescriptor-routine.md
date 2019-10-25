---
title: 記憶域クラス ドライバーの GetDescriptor ルーチン
description: 記憶域クラス ドライバーの GetDescriptor ルーチン
ms.assetid: d1ddcfe8-f276-4e45-82b7-0f07f0526c71
keywords:
- GetDescriptor
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2974409fb82fc47da579ccf2eb342a2c43ae645
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844748"
---
# <a name="storage-class-drivers-getdescriptor-routine"></a>記憶域クラス ドライバーの GetDescriptor ルーチン


## <span id="ddk_storage_class_drivers_getdescriptor_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_GETDESCRIPTOR_ROUTINE_KG"></span>


データ転送操作の場合、記憶域クラスのドライバーには、各 HBA のデバイスが接続されているバスを駆動する構成情報が必要です。 この情報を取得するために、クラスドライバーは内部*Getdescriptor*ルーチンを呼び出すか、または*startdevice*ルーチンで同じ機能を実装します。 ( *Startdevice*の詳細については、「[ストレージクラスドライバーでの PnP 開始の処理](handling-pnp-start-in-a-storage-class-driver.md)」を参照してください)。

*Getdescriptor*ルーチンは、デバイスを取得するためにポートドライバーに対してクエリプロパティ要求 ([**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)を[**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)) を作成および設定します。クラスドライバーがデバイス拡張機能に格納するアダプター記述子。 また、クラスドライバーは、返される記述子データに応じて、デバイス拡張機能でドライバーライターによって決定されたフラグを設定することもあります。

クラスドライバーは、返された[**記憶域\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)データを検査して、デバイスの機能 (scsi の照会データまたはそれと同等ではない scsi) を決定します。たとえば、デバイスのメディア (存在する場合) がリムーバブルであるかどうか (**RemovableMedia**)、デバイスが複数の未処理コマンド (**commandqueueing**) をサポートしているかどうか、およびさまざまな ID 文字列。 クラスドライバーは、返された[**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)データを検査して、次のようなアダプターの機能を決定します。

-   特定の HBA が1回の操作で転送できる最大バイト数 (**Maximumtransferlength**)。

-   連続していない物理ページ (つまり、スキャッター/ギャザーがサポートされている場合) によってバックアップされるバッファー内のデータを転送できる場合は、転送操作ごとに1つのバッファーあたりの連続する物理ページ数を、転送操作ごと (**Maximumphysicalpages**) にします。

-   クラスドライバーがデバイスオブジェクト (配置**マスク**) の配置**要件**フィールドを適切に設定できるように、転送に対する HBA のアラインメント要件。

    IOCTL\_\_SCSI に送信するアプリケーションは、要求に[**よって\_渡す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)ことも、このフィールドを使用する場合があります。

    デバイスオブジェクトでの**要求**の設定の詳細については、「[デバイスオブジェクトの初期化](https://docs.microsoft.com/windows-hardware/drivers/kernel/initializing-a-device-object)」を参照してください。

-   HBA が SCSI タグ付きキューまたは論理ユニットごとの内部キュー (**commandqueueing**) をサポートしているかどうか。

-   HBA が同期転送 (**AcceleratedTransfer**) をサポートしているかどうか。

-   HBA がデータを内部的にキャッシュするかどうか (**Cachesdata**)。

クラスドライバーは、この情報を FDO のデバイス拡張機能に格納する必要があります。これにより、ディスパッチルーチンは、ストレージポートドライバーに送信されるすべての要求が、基になる HBA のサイズ、物理中断の数、およびアラインメントの要件に準拠することを保証できるようになります。 クラスドライバーのディスパッチルーチンの詳細については、「[ストレージクラスドライバーのディスパッチルーチン](storage-class-driver-s-dispatch-routines.md)」を参照してください。 デバイス拡張機能の設定の詳細については、「[ストレージクラスドライバーのデバイス拡張機能](setting-up-a-storage-class-driver-s-device-extension.md)のセットアップ」を参照してください。

 

 




