---
title: 一般 I/O ターゲットの初期化
description: 一般 I/O ターゲットの初期化
ms.assetid: c5d5b589-09a3-4f58-83bf-2876b37b0937
keywords:
- 一般的な I/O WDK KMDF、初期化の対象します。
- WDK KMDF を対象と一般的な I/O の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9d2e5485c2dd5fb9018bc754b78fd0edc6ff3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380562"
---
# <a name="initializing-a-general-io-target"></a>一般 I/O ターゲットの初期化





ドライバーを呼び出すと、フレームワークにドライバーのデバイスのローカル I/O の対象を初期化します[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。 デバイスのローカル I/O ターゲット、ドライバーの呼び出しを識別するハンドルを取得する[ **WdfDeviceGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetiotarget)します。

ほとんどのドライバーでは、そのローカル I/O ターゲットにのみ要求を送信します。

デバイスのリモートの I/O ターゲットを初期化するために、ドライバーが必要です。

1.  呼び出す[ **WdfIoTargetCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetcreate) I/O ターゲット オブジェクトを作成します。

2.  呼び出す[ **WdfIoTargetOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)をドライバーに要求を送信できるように、I/O ターゲットを開きます。

ドライバーを呼び出すと[ **WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)、通常、リモートの I/O ターゲットを表す Unicode 文字列を指定することによって識別、[オブジェクト名](https://docs.microsoft.com/windows-hardware/drivers/kernel/object-names)します。 この名前は、デバイス、ファイル、またはデバイスのインターフェイスを識別できます。 フレームワークは、オブジェクト名をサポートするドライバー スタックの一番上に I/O 要求を送信します。

まれには、ドライバーは Windows Driver Model (WDM) へのポインターを指定してリモート I/O ターゲットを特定可能性があります[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)構造体。 このポインターは、呼び出し元のドライバーのスタック内の別のドライバーを識別します。 フレームワーク ベースのドライバーはこの手法をほとんど使用ほとんど他のドライバーにアクセスしているため**デバイス\_オブジェクト**構造体。

次の例では、Ndisedge サンプル ドライバーが前述の手法を使用して作成し、リモートの I/O ターゲットを開く方法を示しています。

```cpp
status = WdfIoTargetCreate(Adapter->WdfDevice,
                        WDF_NO_OBJECT_ATTRIBUTES,
                        &Adapter->IoTarget);
    if (!NT_SUCCESS(status)) {
        DEBUGP(MP_ERROR, ("WdfIoTargetCreate failed 0x%x\n",
               status));
        return status;
    }

    WDF_IO_TARGET_OPEN_PARAMS_INIT_CREATE_BY_NAME(&openParams,
                                &fileName,
                                STANDARD_RIGHTS_ALL
                                );

    status = WdfIoTargetOpen(Adapter->IoTarget,
                        &openParams);
    if (!NT_SUCCESS(status)) {
        DEBUGP(MP_ERROR, ("WdfIoTargetOpen failed 0x%x\n", status));
        return status;
    }
```

 

 





