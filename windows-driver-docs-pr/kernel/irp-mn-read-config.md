---
title: IRP_MN_READ_CONFIG
description: 構成領域があるバスのバスドライバーは、子デバイス (子 PDOs) に対してこの要求を処理する必要があります。 フィルターおよび関数ドライバーは、この要求を処理しません。
ms.date: 08/12/2017
ms.assetid: cbc5b959-0aae-4c86-b490-296965a7f158
keywords:
- IRP_MN_READ_CONFIG カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: a969bf683b335659b4a8c767f6b43ab97378c111
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827976"
---
# <a name="irp_mn_read_config"></a>IRP\_\_読み取り\_構成


構成領域があるバスのバスドライバーは、子デバイス (子 PDOs) に対してこの要求を処理する必要があります。 フィルターおよび関数ドライバーは、この要求を処理しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

ドライバーまたはその他のシステムコンポーネントが、この IRP を送信して、デバイスの親バスの構成領域を読み取ります。

ドライバーまたはその他のシステムコンポーネントは、任意のスレッドコンテキストでディスパッチ\_レベル &lt;、この IRP を IRQL で送信します。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_STACK\_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の**Parameters. readwriteconfig**メンバー自体は、次の情報を含む構造体です。

```cpp
ULONG WhichSpace;
PVOID Buffer;
ULONG Offset;
ULONG Length
```

構造体のメンバーは、バスドライバーによって異なる方法で解釈できますが、通常、メンバーは次のように定義されます。

<a href="" id="whichspace"></a>**場所**  
アクセスするメモリ領域を指定します。 このパラメーターは次の値を取ることができます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>Bus</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PCI_WHICHSPACE_CONFIG</p></td>
<td><p>PCI</p></td>
<td><p>PCI 構成領域。</p></td>
</tr>
<tr class="even">
<td><p>PCI_WHICHSPACE_ROM</p></td>
<td><p>PCI</p></td>
<td><p>読み取り専用メモリ。</p></td>
</tr>
<tr class="odd">
<td><p>PCCARD_COMMON_MEMORY</p>
<p>PCCARD_COMMON_MEMORY_INDIRECT</p></td>
<td><p>PCMCIA</p></td>
<td><p>メインのカード搭載メモリ。</p></td>
</tr>
<tr class="even">
<td><p>PCCARD_ATTRIBUTE_MEMORY</p>
<p>PCCARD_ATTRIBUTE_MEMORY_INDIRECT</p></td>
<td><p>PCMCIA</p></td>
<td><p>PCMCIA 属性 (構成) 領域。</p></td>
</tr>
<tr class="odd">
<td><p>PCCARD_PCI_CONFIGURATION_SPACE</p></td>
<td><p>PCMCIA</p></td>
<td><p>PCI 構成領域。</p></td>
</tr>
</tbody>
</table>

 

PCI\_*XXX*の値は、Wdm で定義されています。 カード搭載\_*XXX*の値は、Ntddpcm で定義されています。

<a href="" id="buffer"></a>**格納**  
要求された情報を返すバッファーを指します。 IRP を送信するコンポーネントは、ページングされたメモリからこの構造体を割り当てます。 バッファーの形式はバスに固有です。

<a href="" id="offset"></a>**影**  
構成領域へのオフセットを指定します。

<a href="" id="length"></a>**数**  
読み取るバイト数を指定します。

## <a name="output-parameters"></a>出力パラメーター


正常に完了すると、バスドライバーは、要求されたデータを使用して、**パラメーター**にバッファーを読み込みます。

## <a name="io-status-block"></a>I/O ステータス ブロック


バスドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定します。または、STATUS\_INVALID\_PARAMETER\_*n*、STATUS\_no\_デバイスなどの適切なエラー状態に設定します。、または状態\_デバイス\_\_準備ができていません。

正常に完了すると、バスドライバーは**Irp&gt;IoStatus**を、返されたバイト数に設定します。

バスドライバーがこの要求を直ちに完了できない場合は、IRP を保留中としてマークし、戻りステータス\_保留中に設定し、後で IRP を完了することができます。

<a name="operation"></a>操作
---------

バスドライバーは、その子デバイス (子 PDOs) に対してこの IRP を処理します。

関数ドライバーとフィルタードライバーは、この IRP を処理しません。**Irp&gt;IoStatus**を変更せずに、次の下位のドライバーに渡します。状態と、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが設定されていません。

この要求を処理するバスドライバーは、そのドライバーがサポートする値が含まれているかどうかを確認する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

通常、関数ドライバーは、この IRP がアタッチされているデバイススタック内の上位のドライバーに送信され、IRP は親バスドライバーによって処理されます。

Irp の送信の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。 次の手順は、この IRP に特に適用されます。

-   ページングされたプールからバッファーを割り当て、0に初期化します。

-   IRP の次の i/o スタックの場所の値を設定します: set **MajorFunction**を[**irp\_MJ\_PNP**](irp-mj-pnp.md)に設定し、 **minorfunction**を **"irp\_\_\_"** に設定して、適切な値**を設定します。パラメーター。 ReadWriteConfig**。

-   **Iostatus を初期化します。** 状態は状態に\_\_サポートされていません。

-   不要になったときに、IRP とバッファーの割り当てを解除します。

ドライバーは、この IRP を IRQL &lt; ディスパッチ\_レベルから送信する必要があります。

親バスドライバーがこのようなインターフェイスをサポートしている場合、ドライバーは、バスインターフェイスルーチンを使用して、ディスパッチ\_レベルでバスの構成領域にアクセスできます。 バスインターフェイスを取得するために、ドライバーは、ドライバーがアタッチされているデバイススタックに[ **\_インターフェイス要求\_の IRP\_** ](irp-mn-query-interface.md)を送信します。 次に、ドライバーは、インターフェイスで返された適切なルーチンを呼び出します。

たとえば、ディスパッチ\_レベルから構成領域を読み取るために、ドライバーは、ドライバーの初期化時に**IRP\_の\_クエリ\_インターフェイス**を呼び出して、[**バス\_インターフェイス\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)インターフェイスを取得することができます。親バスドライバー。 ドライバーは、IRQL パッシブ\_レベルからクエリの IRP を送信します。 その後、IRQL ディスパッチ\_レベルのコードから、ドライバーはインターフェイスで返される適切なルーチンを呼び出し**ます。たとえば、GetBusData**ルーチンです。

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

[**IRP\_\_書き込み\_構成**](irp-mn-write-config.md)

 

 




