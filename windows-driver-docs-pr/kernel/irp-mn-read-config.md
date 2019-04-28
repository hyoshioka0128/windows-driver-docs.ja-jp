---
title: IRP_MN_READ_CONFIG
description: 構成の領域を持つバスのバス ドライバーには、子デバイス (子 Pdo) は、この要求を処理する必要があります。 ドライバーのフィルターと関数では、この要求は処理しません。
ms.date: 08/12/2017
ms.assetid: cbc5b959-0aae-4c86-b490-296965a7f158
keywords:
- IRP_MN_READ_CONFIG カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 3bb3a95a97e2de5a3c139b7485f9f930da15ec02
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381412"
---
# <a name="irpmnreadconfig"></a>IRP\_MN\_読み取り\_構成


構成の領域を持つバスのバス ドライバーには、子デバイス (子 Pdo) は、この要求を処理する必要があります。 ドライバーのフィルターと関数では、この要求は処理しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

ドライバーやその他のシステム コンポーネントは、デバイスの親のバスの構成領域を読み取るには、この IRP を送信します。

ドライバーやその他のシステム コンポーネントは、IRQL でこの IRP を送信&lt;ディスパッチ\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.ReadWriteConfig**のメンバー、 [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)構造自体は、次を含む構造体情報:

```cpp
ULONG WhichSpace;
PVOID Buffer;
ULONG Offset;
ULONG Length
```

構造体のメンバーは、異なるバス ドライバー、によって異なる方法で解釈されることができますが、メンバーは次のように通常定義します。

<a href="" id="whichspace"></a>**WhichSpace**  
アクセスするには、どのメモリ領域を指定します。 このパラメーターは次の値を取ることができます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>Bus</th>
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
<td><p>メインの pc カード メモリ。</p></td>
</tr>
<tr class="even">
<td><p>PCCARD_ATTRIBUTE_MEMORY</p>
<p>PCCARD_ATTRIBUTE_MEMORY_INDIRECT</p></td>
<td><p>PCMCIA</p></td>
<td><p>PCMCIA 属性 (構成) の領域。</p></td>
</tr>
<tr class="odd">
<td><p>PCCARD_PCI_CONFIGURATION_SPACE</p></td>
<td><p>PCMCIA</p></td>
<td><p>PCI 構成領域。</p></td>
</tr>
</tbody>
</table>

 

PCI\_*XXX*値 Wdm.h で定義されます。 Pc カード\_*XXX*値 Ntddpcm.h で定義されます。

<a href="" id="buffer"></a>**バッファー**  
要求された情報を返すバッファーへのポインター。 IRP を送信するコンポーネントは、ページングされたメモリからこの構造体を割り当てます。 バッファーの形式は、バスに固有です。

<a href="" id="offset"></a>**オフセット**  
構成の領域にオフセットを指定します。

<a href="" id="length"></a>**長さ**  
読み取るバイト数を指定します。

## <a name="output-parameters"></a>出力パラメーター


成功した場合、バス ドライバー バッファーで**Parameters.ReadWriteConfig.Buffer**要求されたデータ。

## <a name="io-status-block"></a>I/O ステータス ブロック


バス ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功や状態などの適切なエラー状態に\_無効な\_パラメーター\_ *n*、状態\_いいえ\_かかる\_デバイス、または状態\_デバイス\_いない\_準備します。

成功した場合、バス ドライバーの設定**Irp -&gt;IoStatus.Information**バイト数が返されます。

バス ドライバーが IRP が保留中のマークの直前に、この要求を完了できない場合は、状態を返す\_保留、後で IRP を完了するとします。

<a name="operation"></a>操作
---------

バス ドライバーでは、その子デバイス (子 Pdo) の場合は、この IRP を処理します。

関数とフィルター ドライバーは、この IRP; を処理しません[次へ] の下位のドライバーに変更を加えるに渡される**Irp -&gt;IoStatus**します。状態と、それらを設定しないでください、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン。

この要求を処理するバス ドライバーには、ドライバーがサポートする値が含まれていることを確認する WhichSpace パラメーターを確認する必要があります。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**この IRP を送信します。**

通常、関数のドライバーでは、先がアタッチされているし、IRP が親のバス ドライバーによって処理されるデバイス スタックの上位のドライバーをこの IRP を送信します。

参照してください[Irp の処理](https://msdn.microsoft.com/library/windows/hardware/ff546847)Irp を送信する方法について。 この IRP に具体的には、次の手順が適用されます。

-   ページ プールからバッファーを確保し、ゼロに初期化します。

-   IRP の I/O スタック内の次の場所の値を設定します設定**MajorFunction**に[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)設定 **。MinorFunction**に**IRP\_MN\_読み取り\_CONFIG**、適切な値を設定し、 **Parameters.ReadWriteConfig**します。

-   初期化**IoStatus.Status**ステータス\_いない\_サポートされています。

-   不要になったときに、IRP とバッファーを解放します。

ドライバーは、IRQL からこの IRP を送信する必要があります&lt;ディスパッチ\_レベル。

ドライバーがディスパッチにバスの構成の領域にアクセスできる\_親バス ドライバーは、このようなインターフェイスをサポートしている場合に、バス インターフェイス ルーチンを通じてレベルします。 バスのインターフェイスを取得するドライバーの送信、 [ **IRP\_MN\_クエリ\_インターフェイス**](irp-mn-query-interface.md)ドライバーが接続されているデバイス スタックを要求します。 ドライバーは、インターフェイスで返される適切なルーチンを呼び出します。

ディスパッチから構成領域を読み取るなど\_レベル、ドライバーが呼び出せる**IRP\_MN\_クエリ\_インターフェイス**を取得するドライバーの初期化中に、 [**BUS\_インターフェイス\_標準**](https://msdn.microsoft.com/library/windows/hardware/ff540707)親バス ドライバーからのインターフェイス。 ドライバーは、IRQL パッシブから IRP のクエリを送信\_レベル。 以降、IRQL のディスパッチにコードから\_レベルなど、インターフェイスで返される適切なルーチンを呼び出すと、ドライバー、 **Interface.GetBusData**ルーチン。

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

## <a name="see-also"></a>関連項目


[**IRP\_MN\_クエリ\_インターフェイス**](irp-mn-query-interface.md)

[**IRP\_MN\_WRITE\_CONFIG**](irp-mn-write-config.md)

 

 




