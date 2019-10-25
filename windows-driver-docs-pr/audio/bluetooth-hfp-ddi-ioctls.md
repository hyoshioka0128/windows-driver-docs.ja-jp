---
title: Bluetooth HFP DDI IOCTLs
description: Windows 8 では、Bluetooth オーディオバイパス接続を操作するために、オーディオドライバーがハンズオンプロファイル (HFP) クラスドライバーで動作できるようにするために、一連の i/o 制御コード (Ioctl) が DDI の一部として導入されています。
ms.assetid: 94B6F113-5130-4772-B8A0-5C9992501824
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d5657f26160f5ccfa45276c4b59c772f826224a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833633"
---
# <a name="bluetooth-hfp-ddi-ioctls"></a>Bluetooth HFP DDI IOCTLs


Windows 8 では、Bluetooth オーディオバイパス接続を操作するために、オーディオドライバーがハンズオンプロファイル (HFP) クラスドライバーで動作できるようにするために、一連の i/o 制御コード (Ioctl) が DDI の一部として導入されています。

特に明記されていない限り、このセクションのすべての Ioctl に対して次のことが当てはまります。

-   要求が成功した場合、状態\_ブロック構造体の情報メンバーは、出力バッファーのサイズ (バイト単位) に設定されます。 それ以外の場合、情報メンバーは0に設定されます。 Status メンバーは、NTSTATUS 値に設定されます。

-   すべての IOCTL は、IRQL &lt;= パッシブ\_レベルを必要とします。

-   オーディオドライバーは、IRP\_MJ\_デバイス\_制御要求で使用する必要があります。

ほとんどの IOCTL 関数コードでは、オーディオドライバーは、hfp ドライバーに送信するデバイスコントロールの IRP を初期化するときに、HFP ドライバーの IO\_スタック\_の場所にある FileObject ポインターを初期化する必要があります。 通常、オーディオドライバーは IoGetDeviceObjectPointer を呼び出すことによってファイルオブジェクトポインターを取得します。

通常、オーディオドライバーは、これらの要求の多くを任意のスレッド (つまり "非同期" 要求) に送信します。 このような場合、オーディオドライバーは IoAllocateIrp メソッドを使用して IRP 自体をビルドし、IoBuildDeviceIoControlRequest を呼び出すのではなく、IRP 内のフィールドを直接設定する必要があります。

次のトピックでは、これらの Windows 8 の Ioctl の詳細について説明します。

[**IOCTL\_BTHHFP\_デバイス\_\_記述子を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)

[**IOCTL\_BTHHFP\_デバイス\_\_VOLUMEPROPERTYVALUES を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_volumepropertyvalues)

[**IOCTL\_BTHHFP\_デバイス\_\_KSNODETYPES を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_ksnodetypes)

[**IOCTL\_BTHHFP\_デバイス\_\_の CONTAINERID を取得する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_containerid)

[**IOCTL\_BTHHFP\_デバイス\_要求\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_connect)

[**IOCTL\_BTHHFP\_デバイス\_要求\_切断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_disconnect)

[**IOCTL\_BTHHFP\_デバイス\_\_接続の取得\_状態\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_connection_status_update)

[**IOCTL\_BTHHFP\_スピーカー\_設定\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_speaker_set_volume)

[**IOCTL\_BTHHFP\_スピーカー\_\_ボリューム\_状態\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_speaker_get_volume_status_update)

[**IOCTL\_BTHHFP\_MIC\_設定\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_mic_set_volume)

[**IOCTL\_BTHHFP\_MIC\_\_ボリュームの取得\_状態\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_mic_get_volume_status_update)

[**IOCTL\_BTHHFP\_ストリーム\_開いています**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_open)

[**IOCTL\_BTHHFP\_ストリーム\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_close)

[**IOCTL\_BTHHFP\_ストリーム\_\_ステータス\_更新を取得する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_get_status_update)

次の新しいものを追加することで、Windows 8.1 が Ioctl のセットを更新しました。

[**IOCTL\_BTHHFP\_デバイス\_\_DESCRIPTOR2 を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor2)

[**IOCTL\_BTHHFP\_デバイス\_を取得\_NRECDISABLE\_状態\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_nrecdisable_status_update)

Windows 10 は、次の新しいものを追加することによって、Ioctl のセットを更新しました。

[**IOCTL\_BTHHFP\_デバイス\_\_コーデック\_ID を取得します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_codec_id)

これらの Ioctl を使用する構造体の詳細については、「 [Bluetooth HFP DDI 構造](bluetooth-hfp-ddi-structures.md)体」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Bluetooth HFP DDI 構造体](bluetooth-hfp-ddi-structures.md)

 

 






