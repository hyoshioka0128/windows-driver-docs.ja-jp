---
title: IRP_MN_QUERY_DEVICE_TEXT
description: PnP マネージャーでは、この IRP を使用して、デバイスの説明または場所の情報を取得します。バスは、この情報をサポートしている場合、バス ドライバーは、子デバイスは、この要求を処理する必要があります。 関数とフィルター ドライバーでは、この IRP は処理されません。
ms.date: 08/12/2017
ms.assetid: 07661709-8929-4567-a05f-96d995862ee6
keywords:
- IRP_MN_QUERY_DEVICE_TEXT カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: eedcf3d55e5e95ee877360a3ded21b914ffe5d45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532817"
---
# <a name="irpmnquerydevicetext"></a>IRP\_MN\_クエリ\_デバイス\_テキスト


PnP マネージャーでは、この IRP を使用して、デバイスの説明または場所の情報を取得します。

バスは、この情報をサポートしている場合、バス ドライバーは、子デバイスは、この要求を処理する必要があります。 関数とフィルター ドライバーでは、この IRP は処理されません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャー送信これらの 2 つの Irp デバイスが列挙されたときに: デバイスの説明、場所情報を照会するもう 1 つのクエリを実行する 1 つ。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.QueryDeviceText.DeviceTextType**のメンバー、 [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)構造体は、 **デバイス\_テキスト\_型**どの文字列が要求を指定する値。 指定できる値**デバイス\_テキスト\_型**含める**DeviceTextDescription**と**DeviceTextLocationInformation**します。

**Parameters.QueryDeviceText.LocaleId** LCID が要求されたテキストのロケールを指定することができます。

## <a name="output-parameters"></a>出力パラメーター


状態の I/O ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態にします。

成功した場合、バス ドライバーの設定**Irp -&gt;IoStatus.Information** WCHAR バッファーに必要な情報を格納しているメモリのドライバーに割り当てられたブロックへのポインター。 バス ドライバーの設定エラーが発生、 **Irp -&gt;IoStatus.Information**をゼロにします。

<a name="operation"></a>操作
---------

バス ドライバーは、子デバイスに対するデバイスの説明を返すよう強くお勧めします。 この文字列に表示されます、**新しいハードウェアが見つかりました**デバイスの INF の一致が検出されない場合、ポップアップ ウィンドウ。

バス ドライバーを返すも推奨**LocationInformation**子も、この情報は省略可能です。 この文字列の形式は、バスに依存します。 デバイス マネージャーには、デバイスの全般プロパティ タブでこの文字列が表示されます。 ベンダーをユーザーに有用な情報を伝える文字列を選択し、サポート担当者する必要があります。 たとえば、PCI、文字列が含まれています、バス、デバイス、および関数。 PC カードは、文字列には、スロットが含まれています。

バス ドライバーでは、この IRP への応答の情報が返された場合、ページングされたメモリから NULL で終わる Unicode 文字列を割り当てます。 PnP マネージャーは、不要になったときに、文字列を解放します。

デバイスの親のバス ドライバーが IRP を完了すると、デバイスが説明または場所の情報を提供しない場合 ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) を変更しなくても**Irp-&gt;IoStatus.Status**または**Irp -&gt;IoStatus.Information**します。

関数とフィルター ドライバーは、この IRP; を処理しません[次へ] の下位のドライバーに変更を加えるに渡される**Irp -&gt;IoStatus**します。

ロケールごとに別のテキスト文字列をサポートするバス ドライバーは、デバイスによって明示的にサポートされていない言語の要求を処理できる必要があります。 このような場合は、バス ドライバーは、最も近いロケールと一致またはフォールバックする必要がありますおよびいくつかサポートされているロケールの適切な文字列を返すを返す必要があります。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**この IRP を送信します。**

システムの使用に予約されています。 ドライバーは、この IRP を送信する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

 

 




