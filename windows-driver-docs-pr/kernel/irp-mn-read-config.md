---
title: IRP_MN_READ_CONFIG
description: 構成領域があるバスのバスドライバーは、子デバイス (子 PDOs) に対してこの要求を処理する必要があります。 フィルターおよび関数ドライバーは、この要求を処理しません。
ms.date: 08/12/2017
ms.assetid: cbc5b959-0aae-4c86-b490-296965a7f158
keywords:
- IRP_MN_READ_CONFIG カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 8dc51a579fb995fc249c0c66dcfba64a3ffdffa6
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922564"
---
# <a name="irp_mn_read_config"></a>IRP\_の\_読み取り\_の構成


構成領域があるバスのバスドライバーは、子デバイス (子 PDOs) に対してこの要求を処理する必要があります。 フィルターおよび関数ドライバーは、この要求を処理しません。

## <a name="value"></a>値

0x0F

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

ドライバーまたはその他のシステムコンポーネントが、この IRP を送信して、デバイスの親バスの構成領域を読み取ります。

ドライバーまたはその他のシステムコンポーネントは、任意&lt;の\_スレッドコンテキストでこの IRP を IRQL ディスパッチレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の構造体の**Parameters. readwriteconfig**メンバー自体は、次の情報を含む構造体です。

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
<th>値</th>
<th>バス</th>
<th>説明</th>
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

 

PCI\_*XXX*の値は、Wdm で定義されています。 カードカード\_*XXX*の値は、Ntddpcm で定義されています。

<a href="" id="buffer"></a>**格納**  
要求された情報を返すバッファーを指します。 IRP を送信するコンポーネントは、ページングされたメモリからこの構造体を割り当てます。 バッファーの形式はバスに固有です。

<a href="" id="offset"></a>**影**  
構成領域へのオフセットを指定します。

<a href="" id="length"></a>**数**  
読み取るバイト数を指定します。

## <a name="output-parameters"></a>出力パラメーター


正常に完了すると、バスドライバーは、要求されたデータを使用して、**パラメーター**にバッファーを読み込みます。

## <a name="io-status-block"></a>I/O ステータス ブロック


バスドライバーは、 **Irp-&gt;iostatus**を、status\_\_\_\_\_\_が SUCCESS に設定されているか、または\_状態\_が*無効*\_であること\_を示す適切なエラー状態を設定します。

成功した場合、バスドライバーは**Irp&gt;-iostatus**を、返されたバイト数に設定します。

バスドライバーがこの要求をすぐに完了できない場合は、IRP を保留中とし\_てマークし、状態を保留中に戻し、後で irp を完了することができます。

<a name="operation"></a>Operation
---------

バスドライバーは、その子デバイス (子 PDOs) に対してこの IRP を処理します。

関数ドライバーとフィルタードライバーは、この IRP を処理しません。**Irp-&gt;iostatus**を変更せずに、次の下位のドライバーに渡します。状態と、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが設定されていません。

この要求を処理するバスドライバーは、そのドライバーがサポートする値が含まれているかどうかを確認する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

通常、関数ドライバーは、この IRP がアタッチされているデバイススタック内の上位のドライバーに送信され、IRP は親バスドライバーによって処理されます。

Irp の送信の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。 次の手順は、この IRP に特に適用されます。

-   ページングされたプールからバッファーを割り当て、0に初期化します。

-   IRP の次の i/o スタックの場所の値を設定します: set **MajorFunction**を[**irp\_MJ\_PNP**](irp-mj-pnp.md)に設定し、 **minorfunction**を**irp\_の\_読み取り\_の構成**に設定して、パラメーターに適切な値を設定し**ます。 readwriteconfig**です。

-   **Iostatus を初期化します。** 状態はサポートされて\_いません\_。

-   不要になったときに、IRP とバッファーの割り当てを解除します。

ドライバーは、この IRP を IRQL &lt;ディスパッチ\_レベルから送信する必要があります。

親バスドライバーがこのようなインターフェイスをサポートし\_ている場合、ドライバーは、バスインターフェイスルーチンを介して、ディスパッチレベルでバスの構成領域にアクセスできます。 バスインターフェイスを取得するために、ドライバーは、ドライバーがアタッチされているデバイススタックに、 [**IRP\_の全\_クエリ\_インターフェイス**](irp-mn-query-interface.md)要求を送信します。 次に、ドライバーは、インターフェイスで返された適切なルーチンを呼び出します。

たとえば\_、ディスパッチレベルから構成領域を読み取るために、ドライバーはドライバーの初期化中に IRP **\_\_\_** を使用したクエリインターフェイスを呼び出し、[**バス\_\_インターフェイスの標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)インターフェイスを親バスドライバーから取得できます。 ドライバーは、IRQL パッシブ\_レベルからクエリの IRP を送信します。 その後、IRQL ディスパッチ\_レベルのコードから、ドライバーはインターフェイスで返された適切なルーチンを呼び出します。たとえば、 **getbusdata**ルーチンです。

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

[**IRP\_の\_全\_書き込みの構成**](irp-mn-write-config.md)

 

 




