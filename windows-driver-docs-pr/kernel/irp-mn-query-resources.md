---
title: IRP_MN_QUERY_RESOURCES
description: PnP マネージャーでは、この IRP を使用して、デバイスのブート構成リソースを取得します。バス ドライバーには、ハードウェア リソースを必要とされる子デバイスは、この要求を処理する必要があります。 関数とフィルター ドライバーでは、この IRP は処理されません。
ms.date: 08/12/2017
ms.assetid: b9a6f06b-07d9-4539-bd41-21cdccdc4b25
keywords:
- IRP_MN_QUERY_RESOURCES Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: e7f88927d772ed26d945456dfd46c6fe2f939af3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381420"
---
# <a name="irpmnqueryresources"></a>IRP\_MN\_クエリ\_リソース


PnP マネージャーでは、この IRP を使用して、デバイスのブート構成リソースを取得します。

バス ドライバーには、ハードウェア リソースを必要とされる子デバイスは、この要求を処理する必要があります。 関数とフィルター ドライバーでは、この IRP は処理されません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーは、デバイスが列挙されたときに、この IRP を送信します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


状態の I/O ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


この IRP を処理するバス ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態にします。

成功した場合、バス ドライバーの設定**Irp -&gt;IoStatus.Information**へのポインターを[ **CM\_リソース\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff541994)を格納しています。要求された情報です。 バス ドライバーの設定エラーが発生、 **Irp -&gt;IoStatus.Information**をゼロにします。

<a name="operation"></a>操作
---------

割り当てるバス ドライバーでは、この IRP への応答でリソースの一覧が返された場合、 [ **CM\_リソース\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff541994)ページングされたメモリから。 PnP マネージャーは、不要になったときにバッファーを解放します。

デバイスの親のバス ドライバーが IRP を完了すると、デバイスにないハードウェア リソースが必要とする場合 ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) を変更しなくても**Irp-&gt;IoStatus.Status**または**Irp -&gt;IoStatus.Information**します。

関数とフィルター ドライバーは、この IRP を受信しません。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**この IRP を送信します。**

システムの使用に予約されています。 ドライバーは、この IRP を送信する必要があります。

ドライバーを呼び出すことができます[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)生と翻訳の両方のフォームで、デバイスのブート構成を取得します。

<a name="requirements"></a>必要条件
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

## <a name="see-also"></a>関連項目


[**CM\_リソース\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff541994)

[**IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)

 

 




