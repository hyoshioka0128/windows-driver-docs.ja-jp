---
title: WMI 登録情報の更新
description: WMI 登録情報の更新
ms.assetid: d24688e5-bb50-4bce-a4d4-4a3bf886f86d
keywords:
- WMI WDK カーネル、WMI への登録
- WMI データプロバイダーの登録
- データプロバイダー WDK WMI
- ドライバー登録 WDK WMI
- イベントブロック WDK WMI
- WDK WMI をブロックする
- 登録 (ブロックを)
- WMI 登録情報を更新しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e8d65d605333c9f6ce08704f7042a2075165046
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836089"
---
# <a name="updating-wmi-registration-information"></a>WMI 登録情報の更新





WMI による最初の登録後、ドライバーは、次のいずれかのアクションを使用して[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出して、登録情報を変更します。

-   WMI REG\_アクションは、ドライバーによって以前に提供されたすべての登録情報を新しい情報に置き換えるために再登録\_ます。

    応答として、WMI は、 [ **\_reginfo**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)要求または[**Irp\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)データパスを持つ reginfo\_EX 要求をドライバーに\_送信します。これは、に設定されています。 (Windows 98 および Windows 2000 では、システムは**IRP\_\_REGINFO**要求を送信します。 Windows XP 以降では、システムが**IRP\_\_REGINFO\_EX**要求に送信します。)

    このドライバーは、サポートされているすべてのブロックの新しい登録情報を WMI に提供します。詳細については、「 [Wmi ライブラリを使用](using-the-wmi-library-to-register-blocks.md)したブロックの登録と[irp\_\_\_\_\_の処理」を参照してください。レジスタブロック](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)。

-   WMI REG\_アクション\_ブロックのサポートを追加または削除したり、登録されているブロックの静的インスタンス名を変更したりするために、\_GUID を更新します。

    応答として、WMI は、 [ **\_reginfo**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[**irp\_データパス\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)要求を、ドライバーに\_送信します。これは、を設定しています。

    ドライバーは、次の更新された登録情報を使用して WMI を提供します。

    -   ドライバーは、このブロックのサポートを削除するために、\_フラグを設定して\_GUID\_削除します。

    -   ドライバーは、\_GUID\_削除して新しいブロックを追加するか、既存のブロックを更新するために、WMI の\_フラグをクリアします。

    -   このドライバーは、インスタンス\_\_インスタンスの\_フラグを設定またはクリアし、必要なインスタンス名情報を指定*して、* ブロックの静的インスタンス名を変更するか、動的インスタンス名を使用するように変更します。

-   Wmi REG\_アクション\_登録を解除して、ドライバーが WMI 情報を提供しなくなることを WMI に指示します。

    WMI は、この呼び出しへの応答として、 **\_reginfo**または**irp\_\_\_** によって出力される irp\_を送信しません。これは、ドライバーに関する情報がこれ以上必要ないからです。 通常、ドライバーは\_デバイスの要求を[**削除\_\_IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)に応答してブロックを解除します。 登録解除呼び出しは、デバイスへのすべての WMI Irp が完了するまでブロックされることに注意してください。 ドライバーが WMI Irp をキューに登録する場合は、 [**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出して登録を解除する前に、それらをキャンセルする必要があります。

 

 




