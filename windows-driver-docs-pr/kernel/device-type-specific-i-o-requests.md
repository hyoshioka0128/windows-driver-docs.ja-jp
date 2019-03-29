---
title: デバイスの種類に固有の I/O 要求
description: デバイスの種類に固有の I/O 要求
ms.assetid: 33ea0b0a-db58-40b7-b6d3-e981acf44dfe
keywords:
- Irp WDK カーネル、デバイスの種類に固有の I/O 要求
- デバイスの種類に固有の I/O 要求の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: df29a43a770745e35576b771c05f6e64e2cf973d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570323"
---
# <a name="device-type-specific-io-requests"></a>デバイスの種類に固有の I/O 要求





Windows Driver Kit (WDK) のデバイスに固有のセクションでは、システム提供の最も一般的な種類のデバイス ドライバーによって処理されるデバイスの種類に固有の I/O 要求に関する情報を提供します。

新しいドライバーは、次の条件のいずれかを満たす場合、新しいカーネル モード ドライバーはシステム提供のドライバーと同じ I/O 要求のセットを処理する必要があります。

-   新しいドライバーには、同じ種類のデバイスのシステム ドライバーが置き換えられます。

-   新しいドライバーは、システムで既に型の別のデバイスをサポートします。

-   新しいドライバーは、2 つのシステム提供のドライバーの間に階層化、中間 (filter) ドライバーです。

このような新しいドライバーを処理する必要がありますすべて**IRP\_MJ\_* XXX*** システム提供のドライバーを処理する要求。 ほとんどの場合、新しいデバイス ドライバも処理の同じセット**IOCTL\_* XXX*** のコードを[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)要求する場合でも、新しいドライバーは、対応するシステム提供のドライバーの動作をエミュレートする必要があります。 それ以外の場合、新しいドライバーは、この種の要求を受け付けるを必要とするユーザー モード アプリケーションを中断する可能性があります。

ドライバーは Irp での I/O の状態のブロックで特定の要求の戻り値として設定できる NTSTATUS 値については、次を参照してください。 [NTSTATUS 値を使用して](using-ntstatus-values.md)します。 エラーのログ パケットに指定できる NTSTATUS 値については、次を参照してください。[ログ エラー](logging-errors.md)します。 新しい種類のデバイス ドライバーによって返される、類似した種類のデバイス、または他、適切な状態の値の決定に役立つ用の新しいドライバーによって返される適切な状態の値を決定するには、この情報を使用します。

ドライバーとそれぞれがサポートするために必要である要求のさまざまな種類の詳細については、次を参照してください。

[シリアル デバイスとドライバー](https://msdn.microsoft.com/library/windows/hardware/ff547451)

[システム提供のパラレル ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff544814)

[記憶装置ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566976)

[HID のアーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/jj126193)

[USB クライアント ドライバーの I/O 要求](https://msdn.microsoft.com/library/windows/hardware/ff540134#km-ioctl)

[IEEE 1394 ドライバー スタック](https://msdn.microsoft.com/library/windows/hardware/ff538867)

[PCMCIA デバイスの属性メモリにアクセスする](https://msdn.microsoft.com/library/windows/hardware/ff536892)

その他のすべての種類のドライバーでは、適切なドライバーの種類のドキュメントを参照してください。

 

 




