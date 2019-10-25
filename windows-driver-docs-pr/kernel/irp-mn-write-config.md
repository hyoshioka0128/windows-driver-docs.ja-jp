---
title: IRP_MN_WRITE_CONFIG
description: 構成領域があるバスのバスドライバーは、子デバイス (子 PDOs) に対してこの要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この要求を処理しません。
ms.date: 08/12/2017
ms.assetid: d57c30b8-83bd-41c9-906d-b8c95f8ca54e
keywords:
- IRP_MN_WRITE_CONFIG カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 59a9e2892f134f883f40e720fff41e34de574f32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827926"
---
# <a name="irp_mn_write_config"></a>IRP\_\_書き込み\_構成


構成領域があるバスのバスドライバーは、子デバイス (子 PDOs) に対してこの要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この要求を処理しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

ドライバーまたはその他のシステムコンポーネントは、この IRP を送信して、デバイスの親バスの構成領域にデータを書き込みます。

ドライバーまたはその他のシステムコンポーネントは、任意のスレッドコンテキストでディスパッチ\_レベル &lt;、この IRP を IRQL で送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. ReadWriteConfig**は、次の情報を含む構造体です。

```cpp
ULONG WhichSpace;
PVOID Buffer;
ULONG Offset;
ULONG Length
```

構造体のメンバーは、バスドライバーによって異なる方法で解釈できますが、通常、メンバーは次のように定義されます。

<a href="" id="whichspace"></a>**場所**  
構成領域を指定します。 **空き領域**として指定できる値の詳細については、「 [**IRP\_\_READ\_CONFIG**](irp-mn-read-config.md)」を参照してください。

<a href="" id="buffer"></a>**格納**  
書き込まれるデータを格納しているバッファーを指します。 バッファーの形式はバスに固有です。

<a href="" id="offset"></a>**影**  
構成領域へのオフセットを指定します。

<a href="" id="length"></a>**数**  
書き込むバイト数を指定します。

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


バスドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定します。または、STATUS\_INVALID\_PARAMETER\_*n*、STATUS\_no\_デバイスなどの適切なエラー状態に設定します。、または状態\_デバイス\_\_準備ができていません。

成功した場合、バスドライバーは**Irp&gt;IoStatus**を、書き込まれたバイト数に設定します。

バスドライバーがこの要求を直ちに完了できない場合は、IRP を保留中としてマークし、戻りステータス\_保留中に設定し、後で IRP を完了することができます。

<a name="operation"></a>操作
---------

バスドライバーは、その子デバイス (子 PDOs) に対してこの IRP を処理します。

関数ドライバーとフィルタードライバーは、この IRP を処理しません。**Irp&gt;IoStatus. Status**を変更せずに次の下位のドライバーに渡し、 [*iostatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定しません。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

通常、関数ドライバーは、この IRP がアタッチされているデバイススタックに送信し、IRP が親バスドライバーによって処理されます。

Irp の送信の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。 次の手順は、この IRP に特に適用されます。

-   ページングされたプールからバッファーを割り当て、書き込まれるデータで初期化します。

-   IRP の次の i/o スタックの場所の値を設定します: set **MajorFunction**を[**irp\_MJ\_PNP**](irp-mj-pnp.md)に設定し、 **minorfunction**を " **irp\_\_** " に設定して、\_構成の適切な値**を設定します。パラメーター。 ReadWriteConfig**。

-   **Iostatus を初期化します。** 状態は状態に\_\_サポートされていません。

-   不要になったときに、IRP とバッファーの割り当てを解除します。

ドライバーは、この IRP を IRQL &lt; ディスパッチ\_レベルから送信する必要があります。

親バスドライバーがそのようなインターフェイスをエクスポートする場合、ドライバーは、バスインターフェイスルーチンを使用して、ディスパッチ\_レベルでバスの構成領域にアクセスできます。 バスインターフェイスを取得するために、ドライバーは、その親バスドライバーに[ **\_インターフェイス要求\_の IRP\_** ](irp-mn-query-interface.md)を送信します。 次に、ドライバーは、インターフェイスで返された適切なルーチンを呼び出します。

たとえば、ディスパッチ\_レベルから構成領域を作成するために、ドライバーは、ドライバーの初期化時に**IRP\_\_クエリ\_インターフェイス**を呼び出して、[**バス\_インターフェイス\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)インターフェイスを取得します。親バスドライバー。 ドライバーは、IRQL パッシブ\_レベルからクエリの IRP を送信します。 その後、IRQL ディスパッチ\_レベルのコードから、ドライバーはインターフェイスで返された適切なルーチンを呼び出し**ます (インターフェイスの SetBusData**ルーチンなど)。

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
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IRP\_\_クエリ\_インターフェイス**](irp-mn-query-interface.md)

[**IRP\_\_読み取り\_構成**](irp-mn-read-config.md)

 

 




