---
title: IRP_MN_QUERY_DEVICE_TEXT
description: PnP マネージャーは、この IRP を使用して、デバイスの説明または場所の情報を取得します。バスがこの情報をサポートしている場合、バスドライバーは、その子デバイスに対してこの要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。
ms.date: 08/12/2017
ms.assetid: 07661709-8929-4567-a05f-96d995862ee6
keywords:
- IRP_MN_QUERY_DEVICE_TEXT カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 11dbdc16e4ce24f23c07d3fd3f37e896bf7607a4
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922480"
---
# <a name="irp_mn_query_device_text"></a>IRP\_の\_全\_クエリ\_のデバイステキスト


PnP マネージャーは、この IRP を使用して、デバイスの説明または場所の情報を取得します。

バスがこの情報をサポートしている場合、バスドライバーは、その子デバイスに対してこの要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。

## <a name="value"></a>値

0x0C

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、デバイスが列挙されると、これらの2つの Irp を送信します。1つはデバイスの説明を照会するもので、もう1つは場所情報を照会するためのものです。

PnP マネージャーは、任意のスレッドコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の**Parameters. Querydevicetext. devicetexttype**メンバーは、要求される文字列を指定する**デバイス\_テキスト\_型**の値です。 **デバイス\_\_テキストの種類**として使用できる値は、 **Devicetextdescription**および**devicetextlocationinformation**です。

**パラメーター**を指定します。 LocaleId は、要求されたテキストのロケールを指定する LCID です。

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp-&gt;iostatus**を、status\_が SUCCESS または適切なエラー状態に設定します。

正常に完了すると、バスドライバーは、要求された情報を持つ WCHAR バッファーを含む、ドライバーによって割り当てられたメモリブロックへのポインターを設定**&gt;します。** エラーが発生した場合、バスドライバーは**Irp-&gt;Iostatus. 情報**を0に設定します。

<a name="operation"></a>Operation
---------

バスドライバーは、子デバイスのデバイスの説明を返すことを強くお勧めします。 この文字列は、デバイスに対して INF の一致が検出されなかった場合に、[**新しいハードウェアが見つかりまし**た] ポップアップウィンドウに表示されます。

バスドライバーでは、子デバイスの**Locationinformation**を返すことも推奨されますが、この情報は省略可能です。 この文字列の形式はバスによって異なります。 デバイスマネージャーは、デバイスの [全般プロパティ] タブにこの文字列を表示します。 ベンダーは、役に立つ情報をユーザーやサポート担当者に伝える文字列を選択する必要があります。 たとえば PCI の場合、文字列にはバス、デバイス、および関数が含まれます。 PC カードの場合、文字列にはスロットが含まれます。

バスドライバーは、この IRP に応答して情報を返す場合、ページングされたメモリから NULL で終わる Unicode 文字列を割り当てます。 不要になった場合は、PnP マネージャーによって文字列が解放されます。

デバイスが説明または場所の情報を提供しない場合、デバイスの親バスドライバーは、irp **-&gt;iostatus. Status**または**Irp-&gt;iostatus. INFORMATION**を変更せずに、irp ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了します。

関数ドライバーとフィルタードライバーは、この IRP を処理しません。**Irp-&gt;iostatus**を変更せずに、次の下位のドライバーに渡します。

ロケールごとに異なるテキスト文字列をサポートするバスのドライバーは、デバイスによって明示的にサポートされていない言語の要求を処理できる必要があります。 このような状況では、バスドライバーはロケールに最も近い一致を返すか、フォールバックして、適切なサポートされているロケール文字列を返す必要があります。

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

 

 




