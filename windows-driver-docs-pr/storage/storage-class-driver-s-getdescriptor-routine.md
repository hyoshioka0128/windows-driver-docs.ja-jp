---
title: 記憶域クラス ドライバーの GetDescriptor ルーチン
description: 記憶域クラス ドライバーの GetDescriptor ルーチン
ms.assetid: d1ddcfe8-f276-4e45-82b7-0f07f0526c71
keywords:
- いる出力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee0b0f5fa489d944f94e7a068340d3ebd60fd29b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368202"
---
# <a name="storage-class-drivers-getdescriptor-routine"></a>記憶域クラス ドライバーの GetDescriptor ルーチン


## <span id="ddk_storage_class_drivers_getdescriptor_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_GETDESCRIPTOR_ROUTINE_KG"></span>


データ転送操作では、記憶域クラス ドライバーには、自分のデバイスが接続されているバスを推進する各 HBA に関する構成情報が必要があります。 この情報を取得するには、クラス ドライバーかを呼び出す内部*いる出力*ルーチンで同じ機能を実装またはその*StartDevice*ルーチン。 (について*StartDevice*を参照してください[、記憶域クラス ドライバーの PnP 開始を処理](handling-pnp-start-in-a-storage-class-driver.md))。

A*いる出力*日常的なビルドや要求のクエリ プロパティを設定 ([**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control) で[**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)) ポート ドライバー クラス ドライバーはそのデバイスに格納されるデバイスとアダプターの記述子を取得するには拡張機能。 クラス ドライバーは、記述子が返されるデータに従って、デバイスの拡張機能でドライバーによりライターで決定されたフラグを設定する可能性がありますもできます。

クラスのドライバーを検査、返された[**ストレージ\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)など、デバイスの機能 (SCSI 問い合わせデータまたは非 SCSI に相当) を決定して、SCSI デバイスの入力 (ある場合)、デバイスのメディアが取り外し可能かどうか (**RemovableMedia**) デバイスが複数の未実行のコマンドをサポートするかどうか、(**CommandQueueing**)、およびさまざまな ID文字列。 クラスのドライバーを検査、返された[**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)データなど、アダプターの機能を決定します。

-   特定の HBA が 1 つの操作で転送できるバイトの最大数 (**MaximumTransferLength**)。

-   HBA を転送できる場合 (つまり、スキャッター/ギャザーをサポートする) 場合、連続しない複数の物理ページによってバッファー内のデータがバックアップされて、バッファーごとを連続していない物理ページ数を管理できる、転送操作あたり (**MaximumPhysicalPages**).

-   転送クラス ドライバーが適切に設定できるように、HBA のアラインメント要件、 **AlignmentRequirement**フィールドにそのデバイス オブジェクト (**AlignmentMask**)。

    送信するアプリケーション[ **IOCTL\_SCSI\_渡す\_を通じて**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)要求もこのフィールドを使用可能性があります。

    設定の詳細については**AlignmentRequirement**でデバイス オブジェクトを参照してください。[デバイス オブジェクトを初期化して](https://docs.microsoft.com/windows-hardware/drivers/kernel/initializing-a-device-object)します。

-   HBA が SCSI のタグ付けされたキューや lun ごとの内部キューをサポートするかどうか (**CommandQueueing**)。

-   HBA が同期転送をサポートするかどうか (**AcceleratedTransfer**)。

-   かどうかのデータをキャッシュ、HBA 内部的に (**CachesData**)。

クラス ドライバーは、サイズ、物理的な改行は、基になる HBA のアラインメント要件の数に記憶域ポート ドライバーに送信されたすべての要求が準拠していること、ディスパッチ ルーチンを確認できるように、FDO のデバイスの拡張機能でこの情報を格納する必要があります。 クラス ドライバーのディスパッチ ルーチンの詳細については、次を参照してください。[記憶域クラス ドライバーのディスパッチ ルーチン](storage-class-driver-s-dispatch-routines.md)します。 デバイスの拡張機能の設定に関する詳細については、次を参照してください。[デバイス拡張機能の設定を、記憶域クラス ドライバーの](setting-up-a-storage-class-driver-s-device-extension.md)します。

 

 




