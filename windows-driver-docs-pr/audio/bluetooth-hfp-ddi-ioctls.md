---
title: Bluetooth HFP DDI IOCTLs
description: Windows 8 では、Bluetooth バイパス オーディオ接続の動作に、ハンズフリー プロファイル (HFP) クラス ドライバーを使用するオーディオ ドライバーを許可する DDI の一部として一連の I/O 制御コード (Ioctl) について説明します。
ms.assetid: 94B6F113-5130-4772-B8A0-5C9992501824
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fd9c072aa55f89a74baa2f46bcc7d96fc03de9d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355612"
---
# <a name="bluetooth-hfp-ddi-ioctls"></a>Bluetooth HFP DDI IOCTLs


Windows 8 では、Bluetooth バイパス オーディオ接続の動作に、ハンズフリー プロファイル (HFP) クラス ドライバーを使用するオーディオ ドライバーを許可する DDI の一部として一連の I/O 制御コード (Ioctl) について説明します。

特に記載がない限り、次に示します。 このセクションでは、すべての Ioctl の場合は true。

-   要求が成功した場合、状態の情報メンバー\_ブロック構造が出力バッファーのバイト単位のサイズに設定されています。 それ以外の場合、情報メンバーは、0 に設定されます。 状態のメンバーは、NTSTATUS 値に設定されます。

-   すべての IOCTL に必要な IRQL &lt;= パッシブ\_レベル。

-   オーディオ ドライバーは IRP に Ioctl を使用する必要があります\_MJ\_デバイス\_コントロール要求。

IOCTL 関数コードのほとんどは、オーディオ ドライバーが、io FileObject ポインターを初期化する必要があります\_スタック\_HFP ドライバー、オーディオ ドライバーは IRP HFP ドライバーに送信するようにデバイスの制御を初期化するときの場所。 通常、オーディオ ドライバーは、IoGetDeviceObjectPointer を呼び出すことによって、ファイル オブジェクト ポインターを取得します。

オーディオ ドライバーは任意のスレッド (つまり、「非同期」の要求) でこれらの要求の多くに送信します。 このような場合は、オーディオ ドライバーは IRP IoAllocateIrp メソッドを使用して自身をビルドして、呼び出し元 IoBuildDeviceIoControlRequest ではなく、直接 IRP のフィールドを設定する必要があります。

これらの Windows 8 Ioctl の詳細については、以下のトピックです。

[**IOCTL\_BTHHFP\_DEVICE\_GET\_DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_VOLUMEPROPERTYVALUES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_volumepropertyvalues)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_KSNODETYPES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_ksnodetypes)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_CONTAINERID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_containerid)

[**IOCTL\_BTHHFP\_DEVICE\_REQUEST\_CONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_connect)

[**IOCTL\_BTHHFP\_デバイス\_要求\_切断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_disconnect)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_CONNECTION\_STATUS\_UPDATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_connection_status_update)

[**IOCTL\_BTHHFP\_スピーカー\_設定\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_speaker_set_volume)

[**IOCTL\_BTHHFP\_SPEAKER\_GET\_VOLUME\_STATUS\_UPDATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_speaker_get_volume_status_update)

[**IOCTL\_BTHHFP\_MIC\_SET\_VOLUME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_mic_set_volume)

[**IOCTL\_BTHHFP\_MIC\_GET\_VOLUME\_STATUS\_UPDATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_mic_get_volume_status_update)

[**IOCTL\_BTHHFP\_STREAM\_OPEN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_open)

[**IOCTL\_BTHHFP\_STREAM\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_close)

[**IOCTL\_BTHHFP\_STREAM\_GET\_STATUS\_UPDATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_get_status_update)

Windows 8.1 では、Ioctl のセットを次の新しいものを追加することで更新します。

[**IOCTL\_BTHHFP\_DEVICE\_GET\_DESCRIPTOR2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor2)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_NRECDISABLE\_STATUS\_UPDATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_nrecdisable_status_update)

Windows 10 では、次の新しいサブスクリプションを追加して Ioctl のセットが更新します。

[**IOCTL\_BTHHFP\_DEVICE\_GET\_CODEC\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_codec_id)

これらの Ioctl で動作する構造については、次を参照してください。 [Bluetooth HFP DDI 構造](bluetooth-hfp-ddi-structures.md)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Bluetooth HFP DDI 構造体](bluetooth-hfp-ddi-structures.md)

 

 






