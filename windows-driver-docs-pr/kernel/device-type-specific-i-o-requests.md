---
title: デバイスの種類に固有の i/o 要求
description: デバイスの種類に固有の i/o 要求
ms.assetid: 33ea0b0a-db58-40b7-b6d3-e981acf44dfe
keywords:
- Irp WDK カーネル、デバイスの種類に固有の i/o 要求
- デバイスの種類に固有の i/o 要求 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d55a7fd1baef45ae1190102de826a636a2e8673
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838739"
---
# <a name="device-type-specific-io-requests"></a>デバイスの種類に固有の i/o 要求





Windows Driver Kit (WDK) のデバイス固有のセクションには、最も一般的な種類のデバイスに対してシステムが提供するドライバーによって処理される、デバイスの種類に固有の i/o 要求に関する情報が記載されています。

新しいドライバーが次のいずれかの条件を満たしている場合、新しいカーネルモードドライバーでは、システム提供のドライバーと同じ i/o 要求セットを処理する必要があります。

-   新しいドライバーにより、同じ種類のデバイスのシステムドライバーが置き換えられます。

-   新しいドライバーは、システムに既に存在する種類の別のデバイスをサポートしています。

-   新しいドライバーは、2つのシステムが提供するドライバー間で階層化された中間 (フィルター) ドライバーです。

この新しいドライバーでは、システム提供のドライバーが処理するすべての**IRP\_MJ\_* XXX*** 要求を処理する必要があります。 ほとんどの場合、新しいデバイスドライバーでは、 [**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求に対して同じ**IOCTL\_* XXX*** コードを処理する必要があります。これは、新しいドライバーが対応するの動作をエミュレートする必要がある場合でも同様です。システムが提供するドライバー。 そうしないと、新しいドライバーは、このような要求が受け入れられるユーザーモードアプリケーションを中断する可能性があります。

ドライバーが Irp の i/o 状態ブロックで設定できる NTSTATUS 値については、特定の要求の戻り値として、「 [Ntstatus 値の使用](using-ntstatus-values.md)」を参照してください。 エラーログパケットで指定できる NTSTATUS 値の詳細については、「[ログエラー](logging-errors.md)」を参照してください。 この情報を使用して、類似した種類のデバイスの新しいドライバーによって返される適切な状態値を決定したり、新しい種類のデバイスのドライバーから返される適切なステータス値を決定したりすることができます。

さまざまな種類のドライバーと、それぞれがサポートする必要がある要求の詳細については、次を参照してください。

[シリアルデバイスとドライバー](https://docs.microsoft.com/previous-versions/ff547451(v=vs.85))

[システム提供のパラレルドライバー](https://docs.microsoft.com/previous-versions/ff544814(v=vs.85))

[記憶域ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)

[HID アーキテクチャ](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85))

[USB クライアントドライバーに対する i/o 要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#km-ioctl)

[IEEE 1394 ドライバースタック](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)

[PCMCIA デバイスの属性メモリにアクセスする](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-attribute-memory-of-a-pcmcia-device)

その他の種類のドライバーについては、該当するドライバーの種類のドキュメントを参照してください。

 

 




