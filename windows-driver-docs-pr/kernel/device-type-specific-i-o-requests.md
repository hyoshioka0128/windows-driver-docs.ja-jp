---
title: デバイスの種類に固有の I/O 要求
description: デバイスの種類に固有の I/O 要求
ms.assetid: 33ea0b0a-db58-40b7-b6d3-e981acf44dfe
keywords:
- Irp WDK カーネル、デバイスの種類に固有の I/O 要求
- デバイスの種類に固有の I/O 要求の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88761c3b76aed408a41cbfaad39384123d5d95a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385005"
---
# <a name="device-type-specific-io-requests"></a>デバイスの種類に固有の I/O 要求





Windows Driver Kit (WDK) のデバイスに固有のセクションでは、システム提供の最も一般的な種類のデバイス ドライバーによって処理されるデバイスの種類に固有の I/O 要求に関する情報を提供します。

新しいドライバーは、次の条件のいずれかを満たす場合、新しいカーネル モード ドライバーはシステム提供のドライバーと同じ I/O 要求のセットを処理する必要があります。

-   新しいドライバーには、同じ種類のデバイスのシステム ドライバーが置き換えられます。

-   新しいドライバーは、システムで既に型の別のデバイスをサポートします。

-   新しいドライバーは、2 つのシステム提供のドライバーの間に階層化、中間 (filter) ドライバーです。

このような新しいドライバーを処理する必要がありますすべて**IRP\_MJ\_* XXX*** システム提供のドライバーを処理する要求。 ほとんどの場合、新しいデバイス ドライバも処理の同じセット**IOCTL\_* XXX*** のコードを[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求する場合でも、新しいドライバーは、対応するシステム提供のドライバーの動作をエミュレートする必要があります。 それ以外の場合、新しいドライバーは、この種の要求を受け付けるを必要とするユーザー モード アプリケーションを中断する可能性があります。

ドライバーは Irp での I/O の状態のブロックで特定の要求の戻り値として設定できる NTSTATUS 値については、次を参照してください。 [NTSTATUS 値を使用して](using-ntstatus-values.md)します。 エラーのログ パケットに指定できる NTSTATUS 値については、次を参照してください。[ログ エラー](logging-errors.md)します。 新しい種類のデバイス ドライバーによって返される、類似した種類のデバイス、または他、適切な状態の値の決定に役立つ用の新しいドライバーによって返される適切な状態の値を決定するには、この情報を使用します。

ドライバーとそれぞれがサポートするために必要である要求のさまざまな種類の詳細については、次を参照してください。

[シリアル デバイスとドライバー](https://docs.microsoft.com/previous-versions/ff547451(v=vs.85))

[システム提供のパラレル ドライバー](https://docs.microsoft.com/previous-versions/ff544814(v=vs.85))

[記憶装置ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)

[HID のアーキテクチャ](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85))

[USB クライアント ドライバーの I/O 要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#km-ioctl)

[IEEE 1394 ドライバー スタック](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)

[PCMCIA デバイスの属性メモリにアクセスする](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-attribute-memory-of-a-pcmcia-device)

その他のすべての種類のドライバーでは、適切なドライバーの種類のドキュメントを参照してください。

 

 




