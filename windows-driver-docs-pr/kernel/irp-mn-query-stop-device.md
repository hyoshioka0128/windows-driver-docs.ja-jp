---
title: IRP_MN_QUERY_STOP_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 22f58964-23a0-4307-a748-9c1620e30871
keywords:
- IRP_MN_QUERY_STOP_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: df734894a12efe91ae0257aa03ff95b07382d992
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922523"
---
# <a name="irp_mn_query_stop_device"></a>IRP\_の\_全\_クエリ\_の停止デバイス


すべての PnP ドライバーは、この IRP を処理する必要があります。

## <a name="value"></a>値

0x05

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、この IRP を送信して、リソースを再調整するためにデバイスを停止できるかどうかを照会します。

Windows 98/Me では、デバイスが無効になっているときにも、PnP マネージャーによってこの IRP が送信されます。

PnP マネージャーは、システムスレッドのコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


None

## <a name="output-parameters"></a>出力パラメーター


None

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp-&gt;iostatus**を、status\_が SUCCESS または適切なエラー状態に設定します。 ドライバーがデバイスを停止できない場合、ドライバーは**Irp-&gt;iostatus**を status に\_設定します。

バスドライバーでは、 **irp-&gt;iostatus**を\_\_設定できます。状態\_は、irp の成功を示すように変更されました。また、PnP マネージャーがデバイスのリソース要件を再実行してから、stop Irp を送信するように要求することもできます。

<a name="operation"></a>Operation
---------

この IRP は、デバイススタックの一番上にあるドライバーによって最初に処理され、スタック内の下位の各ドライバーに渡されます。

この IRP に応答して、Windows 2000 以降のドライバーは、リソースの再調整のためにデバイスを安全に停止できるかどうかを示します。

Windows 98/Me では、この IRP はリソースの再調整時だけでなく、デバイスが無効になっているときにも送信されます。 ドライバーはこれらの2つの状況を区別できないため、デバイスが無効になっているかのように処理を続行する必要があります。 デバイスに対して開いているハンドルがある場合、ドライバーはこの IRP を失敗させる必要があります。 ハンドルが開いていない場合は、「 [IRP\_の全\_クエリ\_の停止\_デバイス要求の処理 (Windows 98/Me)](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-query-stop-device-request--windows-98-me-)」で説明されているように、ドライバーを続行する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システムで使用するために予約されています。 ドライバーは、この IRP を送信することはできません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**\_IRP\_が\_終了し\_たときにデバイスを停止する**](irp-mn-cancel-stop-device.md)

[**IRP\_\_デバイス\_使用量\_の通知**](irp-mn-device-usage-notification.md)

[**IRP\_の\_全\_開始デバイス**](irp-mn-start-device.md)

[**IRP\_の\_全\_停止デバイス**](irp-mn-stop-device.md)

 

 




