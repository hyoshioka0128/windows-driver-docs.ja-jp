---
title: IRP_MN_WRITE_CONFIG
description: 構成領域があるバスのバスドライバーは、子デバイス (子 PDOs) に対してこの要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この要求を処理しません。
ms.date: 08/12/2017
ms.assetid: d57c30b8-83bd-41c9-906d-b8c95f8ca54e
keywords:
- IRP_MN_WRITE_CONFIG カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 2070ed7b0927da2d230924921af17aa5edb54361
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922549"
---
# <a name="irp_mn_write_config"></a>IRP\_の\_全\_書き込みの構成


構成領域があるバスのバスドライバーは、子デバイス (子 PDOs) に対してこの要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この要求を処理しません。

## <a name="value"></a>値

0x10

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

ドライバーまたはその他のシステムコンポーネントは、この IRP を送信して、デバイスの親バスの構成領域にデータを書き込みます。

ドライバーまたはその他のシステムコンポーネントは、任意&lt;の\_スレッドコンテキストでこの IRP を IRQL ディスパッチレベルで送信します。

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
構成領域を指定します。 **領域**に対して指定できる値の詳細については、「 [**IRP\_の\_読み取り\_の構成**](irp-mn-read-config.md)」を参照してください。

<a href="" id="buffer"></a>**格納**  
書き込まれるデータを格納しているバッファーを指します。 バッファーの形式はバスに固有です。

<a href="" id="offset"></a>**影**  
構成領域へのオフセットを指定します。

<a href="" id="length"></a>**数**  
書き込むバイト数を指定します。

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


バスドライバーは、 **Irp-&gt;iostatus**を、status\_\_\_\_\_\_が SUCCESS に設定されているか、または\_状態\_が*無効*\_であること\_を示す適切なエラー状態を設定します。

成功した場合、バスドライバーは**Irp&gt;-iostatus**を、書き込まれたバイト数に設定します。

バスドライバーがこの要求を直ちに完了できない場合は、IRP を保留中とし\_てマークし、状態を保留中に戻して、後で irp を完了することができます。

<a name="operation"></a>Operation
---------

バスドライバーは、その子デバイス (子 PDOs) に対してこの IRP を処理します。

関数ドライバーとフィルタードライバーは、この IRP を処理しません。**Irp-&gt;Iostatus. Status**を変更せずに次の下位のドライバーに渡し、 [*iostatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定しません。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

通常、関数ドライバーは、この IRP がアタッチされているデバイススタックに送信し、IRP が親バスドライバーによって処理されます。

Irp の送信の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。 次の手順は、この IRP に特に適用されます。

-   ページングされたプールからバッファーを割り当て、書き込まれるデータで初期化します。

-   IRP の次の i/o スタックの場所の値を設定します: set **MajorFunction**を[**irp\_MJ\_PNP**](irp-mj-pnp.md)に設定し、 **minorfunction**を Irp **\_\_\_** による書き込みの構成に設定し、パラメーターに適切な値を設定し**ます。 readwriteconfig**です。

-   **Iostatus を初期化します。** 状態はサポートされて\_いません\_。

-   不要になったときに、IRP とバッファーの割り当てを解除します。

ドライバーは、この IRP を IRQL &lt;ディスパッチ\_レベルから送信する必要があります。

親バスドライバーがそのようなインターフェイスをエクスポートする\_場合、ドライバーは、バスインターフェイスルーチンを介して、ディスパッチレベルでバスの構成領域にアクセスできます。 バスインターフェイスを取得するために、ドライバーは、その親バスドライバーに対して[**IRP\_を実行する\_クエリ\_インターフェイス**](irp-mn-query-interface.md)要求を送信します。 次に、ドライバーは、インターフェイスで返された適切なルーチンを呼び出します。

たとえば\_、ディスパッチレベルから構成領域を書き込むために、ドライバーはドライバーの初期化時に IRP **\_の\_全クエリ\_インターフェイス**を呼び出して、[**バス\_インターフェイス\_の標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)インターフェイスを親バスドライバーから取得できます。 ドライバーは、IRQL パッシブ\_レベルからクエリの IRP を送信します。 その後、IRQL ディスパッチ\_レベルのコードから、ドライバーはインターフェイスで返された適切なルーチンを呼び出します (インターフェイスの**setbusdata**ルーチンなど)。

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


[**IRP\_の\_全\_クエリインターフェイス**](irp-mn-query-interface.md)

[**IRP\_の\_読み取り\_の構成**](irp-mn-read-config.md)

 

 




