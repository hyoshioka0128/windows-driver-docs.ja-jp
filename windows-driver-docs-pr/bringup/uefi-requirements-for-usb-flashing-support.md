---
title: USB サポートが点滅の UEFI 要件
description: Microsoft は、エンジニア リングと、製造環境で使用するためのいくつかの USB ベースの点滅ソリューションを提供します。 これらのツールで使用するデバイスで、デバイスの UEFI 環境は、このトピックに記載の要件を満たす必要があります。
ms.assetid: 8979173C-DCBC-4544-9978-BB069FF35914
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 088b3b8c2ea0c30c1b3cf9bae9676bbb60614d7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551467"
---
# <a name="uefi-requirements-for-usb-flashing-support"></a>USB サポートが点滅の UEFI 要件

Microsoft は、エンジニア リングと、製造環境で使用するためのいくつかの USB ベースの点滅ソリューションを提供します。 これらのツールで使用するデバイスで、デバイスの UEFI 環境は、このトピックに記載の要件を満たす必要があります。

点滅に関連するこれらの要件の展開での UEFI 要件[Windows のすべてのエディションに適用される UEFI 要件](uefi-requirements-that-apply-to-all-windows-platforms.md)と[Windows 10 Mobile の UEFI 要件](uefi-requirements-specific-to-windows-mobile.md)します。

## <a name="required-uefi-protocols"></a>UEFI の必要なプロトコル

| プロトコル | 要件の詳細 |
| --- | --- |
| USB 関数プロトコル | ファームウェアの USB 3.0 を経由して、usb、UEFI USB 関数プロトコル改訂 0x00010002 またはより高いサポート実装する必要があります、 [EFI\_USBFN\_IO\_プロトコル。ConfigureEnableEndpointsEx](efi-usbfn-io-protocol-configureenableendpointsex.md)関数。 詳細については、次を参照してください。 [UEFI USB 関数プロトコル](uefi-usb-function-protocol.md)します。 |
| Blockio の相対的 | Microsoft 提供の USB 点滅ソリューションでは、点滅の非ゼロ I/O サイズのブロック ストレージ デバイスに最初に返されたポインターを選択します。 デバイスは、固定またはリムーバブル記憶域を指定できます。                                                                                                                                                             |
## <a name="uefi-desync-event-optional"></a>UEFI desync イベント (省略可能)

読み取りを試みますまたはフラッシュ中にディスクに書き込みを UEFI コンポーネントは、UEFI desync イベントのサポートを実装する必要があります (EFI\_イベント\_グループ\_ファームウェア\_DESYNC) 次の表で説明します。

| 要件 | 説明 |
| --- | --- |
| UEFI ブート サービスのサポート | UEFI ファームウェアは、タイマー、イベントをサポートする必要があり、タスクの優先順位のサービスで定義されているセクション 6.1 UEFI 2.3.1 の仕様。 |
| イベント グループの GUID | Microsoft には、次の GUID を持つ EFI_EVENT_GROUP_FIRMWARE_DESYNC が定義されています: {24FA5E72-1A82-49A2-970B-3230372662A5} |
| UEFI ファームウェア イベント | 更新または同期の状態を定期的に記憶域のバックアップを必要とするすべての UEFI ファームウェア コンポーネントを特定します。 これらのコンポーネントの各で、EFI_EVENT_GROUP_FIRMWARE_DESYNC と記憶域に更新する同期を停止する対象のコンポーネントを原因となる NotifyFunction() に関連付けられたイベントを作成します。 イベントの NotifyFunction() には、コンポーネントの desynchronized モードに移行するために必要なクリーンアップ操作を実行する必要があります。 このクリーンアップでは、後に、コンポーネントを更新または flash でその記憶域を次のデバイスの再起動まで同期されません。 イベントの NotifyFunction fails()、NotifyFunction() EFI_SUCCESS が返されなかった必要がある場合。 |

次のコード例では、ファームウェアでしたイベント グループ GUID を作成する方法を示します。

```cpp
gBS->CreateEventEx (
    EVT_NOTIFY_SIGNAL,
    TPL_CALLBACK,
    FIRMWARE_NOTIFICATION_FUNCTION,          // To be defined by SoC Vendor
    &FIRMWARE_NOTIFICATION_FUNCTION_CONTEXT, // To be defined by SoC Vendor
    &EFI_EVENT_GROUP_FIRMWARE_DESYNC,
    &Event                                   // Event returned by CreateEventEx
);
```

## <a name="related-topics"></a>関連トピック

[SoC のプラットフォームで Windows の最小の UEFI 要件](minimum-uefi-requirements-for-windows-on-soc-platforms.md)  

[すべての Windows エディションに適用される UEFI 要件](uefi-requirements-that-apply-to-all-windows-platforms.md)  

[Windows 10 Mobile の UEFI 要件](uefi-requirements-specific-to-windows-mobile.md)  
