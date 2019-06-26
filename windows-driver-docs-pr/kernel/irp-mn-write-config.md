---
title: IRP_MN_WRITE_CONFIG
description: 構成の領域を持つバスのバス ドライバーには、子デバイス (子 Pdo) は、この要求を処理する必要があります。 関数とフィルター ドライバーでは、この要求は処理しません。
ms.date: 08/12/2017
ms.assetid: d57c30b8-83bd-41c9-906d-b8c95f8ca54e
keywords:
- IRP_MN_WRITE_CONFIG Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: b12c949ad7a4ef2f3c56d242645d1aefb77d7176
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376453"
---
# <a name="irpmnwriteconfig"></a>IRP\_MN\_書き込み\_構成


構成の領域を持つバスのバス ドライバーには、子デバイス (子 Pdo) は、この要求を処理する必要があります。 関数とフィルター ドライバーでは、この要求は処理しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

ドライバーやその他のシステム コンポーネントは、デバイスの親のバスの構成領域にデータを書き込むには、この IRP を送信します。

ドライバーやその他のシステム コンポーネントは、IRQL でこの IRP を送信&lt;ディスパッチ\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.ReadWriteConfig**は、次の情報を格納している構造体です。

```cpp
ULONG WhichSpace;
PVOID Buffer;
ULONG Offset;
ULONG Length
```

構造体のメンバーは、異なるバス ドライバー、によって異なる方法で解釈されることができますが、メンバーは次のように通常定義します。

<a href="" id="whichspace"></a>**WhichSpace**  
構成の領域を指定します。 指定できる値について**WhichSpace**を参照してください[ **IRP\_MN\_読み取り\_CONFIG**](irp-mn-read-config.md)します。

<a href="" id="buffer"></a>**バッファー**  
書き込むデータを格納しているバッファーへのポインター。 バッファーの形式は、バスに固有です。

<a href="" id="offset"></a>**オフセット**  
構成の領域にオフセットを指定します。

<a href="" id="length"></a>**長さ**  
書き込むバイト数を指定します。

## <a name="output-parameters"></a>出力パラメーター


状態の I/O ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


バス ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功や状態などの適切なエラー状態に\_無効な\_パラメーター\_ *n*、状態\_いいえ\_かかる\_デバイス、または状態\_デバイス\_いない\_準備します。

成功した場合、バス ドライバーの設定**Irp -&gt;IoStatus.Information**に書き込まれたバイト数。

バス ドライバーは、この要求をすぐに完了できない場合、保留中の IRP をマーク、状態を返す\_保留、後で IRP を完了するとします。

<a name="operation"></a>操作
---------

バス ドライバーでは、その子デバイス (子 Pdo) の場合は、この IRP を処理します。

関数とフィルター ドライバーは、この IRP; を処理しません[次へ] の下位のドライバーに変更を加えるに渡される**Irp -&gt;IoStatus.Status**を設定しないと、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン。

参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**この IRP を送信します。**

通常、関数のドライバーでは、デバイス スタックがアタッチされているし、IRP が親のバス ドライバーによって処理されるをこの IRP を送信します。

参照してください[Irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)Irp を送信する方法について。 この IRP に具体的には、次の手順が適用されます。

-   ページ プールからバッファーを割り当て、書き込まれるデータで初期化します。

-   IRP の I/O スタック内の次の場所の値を設定します設定**MajorFunction**に[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)設定 **。MinorFunction**に**IRP\_MN\_書き込み\_CONFIG**、適切な値を設定し、 **Parameters.ReadWriteConfig**します。

-   初期化**IoStatus.Status**ステータス\_いない\_サポートされています。

-   不要になったときに、IRP とバッファーを解放します。

ドライバーは、IRQL からこの IRP を送信する必要があります&lt;ディスパッチ\_レベル。

ドライバーがディスパッチにバスの構成の領域にアクセスできる\_を通じて、バス インターフェイス ルーチンでは、レベルの親のバス ドライバーは、このようなインターフェイスをエクスポートする場合。 バスのインターフェイスを取得するドライバーの送信、 [ **IRP\_MN\_クエリ\_インターフェイス**](irp-mn-query-interface.md)その親のバス ドライバーに要求します。 ドライバーは、インターフェイスで返される適切なルーチンを呼び出します。

例では、ディスパッチから構成領域を書き込む\_レベルのドライバーを呼び出すことができます**IRP\_MN\_クエリ\_インターフェイス**を取得するドライバーの初期化中に、 [**BUS\_インターフェイス\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_bus_interface_standard)親バス ドライバーからのインターフェイス。 ドライバーは、IRQL パッシブから IRP のクエリを送信\_レベル。 以降、IRQL のディスパッチにコードから\_レベルなど、インターフェイスで返される適切なルーチンを呼び出すと、ドライバー、 **Interface.SetBusData**ルーチン。

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


[**IRP\_MN\_クエリ\_インターフェイス**](irp-mn-query-interface.md)

[**IRP\_MN\_READ\_CONFIG**](irp-mn-read-config.md)

 

 




