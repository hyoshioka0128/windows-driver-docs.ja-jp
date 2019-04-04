---
title: 記憶域クラス ドライバーいる出力ルーチン
description: 記憶域クラス ドライバーいる出力ルーチン
ms.assetid: d1ddcfe8-f276-4e45-82b7-0f07f0526c71
keywords:
- いる出力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f3f439c1fd1a72561cb5c25adf8e8158b94de8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558451"
---
# <a name="storage-class-drivers-getdescriptor-routine"></a>記憶域クラス ドライバーいる出力ルーチン


## <span id="ddk_storage_class_drivers_getdescriptor_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_GETDESCRIPTOR_ROUTINE_KG"></span>


データ転送操作では、記憶域クラス ドライバーには、自分のデバイスが接続されているバスを推進する各 HBA に関する構成情報が必要があります。 この情報を取得するには、クラス ドライバーかを呼び出す内部*いる出力*ルーチンで同じ機能を実装またはその*StartDevice*ルーチン。 (について*StartDevice*を参照してください[、記憶域クラス ドライバーの PnP 開始を処理](handling-pnp-start-in-a-storage-class-driver.md))。

A*いる出力*日常的なビルドや要求のクエリ プロパティを設定 ([**IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744) で[**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff560590)) ポート ドライバー クラス ドライバーはそのデバイスに格納されるデバイスとアダプターの記述子を取得するには拡張機能。 クラス ドライバーは、記述子が返されるデータに従って、デバイスの拡張機能でドライバーによりライターで決定されたフラグを設定する可能性がありますもできます。

クラスのドライバーを検査、返された[**ストレージ\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566971)など、デバイスの機能 (SCSI 問い合わせデータまたは非 SCSI に相当) を決定して、SCSI デバイスの入力 (ある場合)、デバイスのメディアが取り外し可能かどうか (**RemovableMedia**) デバイスが複数の未実行のコマンドをサポートするかどうか、(**CommandQueueing**)、およびさまざまな ID文字列。 クラスのドライバーを検査、返された[**ストレージ\_アダプター\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566346)データなど、アダプターの機能を決定します。

-   特定の HBA が 1 つの操作で転送できるバイトの最大数 (**MaximumTransferLength**)。

-   HBA を転送できる場合 (つまり、スキャッター/ギャザーをサポートする) 場合、連続しない複数の物理ページによってバッファー内のデータがバックアップされて、バッファーごとを連続していない物理ページ数を管理できる、転送操作あたり (**MaximumPhysicalPages**).

-   転送クラス ドライバーが適切に設定できるように、HBA のアラインメント要件、 **AlignmentRequirement**フィールドにそのデバイス オブジェクト (**AlignmentMask**)。

    送信するアプリケーション[ **IOCTL\_SCSI\_渡す\_を通じて**](https://msdn.microsoft.com/library/windows/hardware/ff560519)要求もこのフィールドを使用可能性があります。

    設定の詳細については**AlignmentRequirement**でデバイス オブジェクトを参照してください。[デバイス オブジェクトを初期化して](https://msdn.microsoft.com/library/windows/hardware/ff547807)します。

-   HBA が SCSI のタグ付けされたキューや lun ごとの内部キューをサポートするかどうか (**CommandQueueing**)。

-   HBA が同期転送をサポートするかどうか (**AcceleratedTransfer**)。

-   かどうかのデータをキャッシュ、HBA 内部的に (**CachesData**)。

クラス ドライバーは、サイズ、物理的な改行は、基になる HBA のアラインメント要件の数に記憶域ポート ドライバーに送信されたすべての要求が準拠していること、ディスパッチ ルーチンを確認できるように、FDO のデバイスの拡張機能でこの情報を格納する必要があります。 クラス ドライバーのディスパッチ ルーチンの詳細については、[記憶域クラス ドライバーのディスパッチ ルーチン](storage-class-driver-s-dispatch-routines.md)を参照してください。 デバイスの拡張機能の設定に関する詳細については、[デバイス拡張機能の設定を、記憶域クラス ドライバーの](setting-up-a-storage-class-driver-s-device-extension.md)を参照してください。

 

 




