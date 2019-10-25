---
title: その他の規則セット (WDM)
description: これらの規則を使用して、ドライバーがレジストリキー、文字列、およびデバイスオブジェクトポインターを適切に処理するための一般的な要件のセットに正しく従っていることを確認します。
ms.assetid: 50E8BFFE-AC38-4023-9FFB-DC53B749A603
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 534aa104a9fe72feae86e5c926507b543e2fd9fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839407"
---
# <a name="miscellaneous-rule-set-wdm"></a>その他の規則セット (WDM)


これらの規則を使用して、ドライバーがレジストリキー、文字列、およびデバイスオブジェクトポインターを適切に処理するための一般的な要件のセットに正しく従っていることを確認します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wdm-adddevice.md" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](wdm-adddevice.md)"><strong>AddDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-adddevice.md" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](wdm-adddevice.md)"><strong>AddDevice</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)"><strong>IoCreateDevice</strong></a>を呼び出した後にのみ、ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><strong>AddDevice</strong></a>ルーチンが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)"><strong>ioattachdevicetodevicestack</strong></a>を呼び出すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-danglingdeviceobjectreference.md" data-raw-source="[&lt;strong&gt;DanglingDeviceObjectReference&lt;/strong&gt;](wdm-danglingdeviceobjectreference.md)"><strong>DanglingDeviceObjectReference</strong></a></p></td>
<td align="left"><p><a href="wdm-danglingdeviceobjectreference.md" data-raw-source="[&lt;strong&gt;DanglingDeviceObjectReference&lt;/strong&gt;](wdm-danglingdeviceobjectreference.md)"><strong>DanglingDeviceObjectReference</strong></a>規則は、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference" data-raw-source="[&lt;strong&gt;IoGetAttachedDeviceReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)"><strong>IoGetAttachedDeviceReference</strong></a>から返されたものと同じデバイスオブジェクトポインターを使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)"><strong>ObDereferenceObject</strong></a>を呼び出すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpsamedeviceobject.md" data-raw-source="[&lt;strong&gt;PnpSameDeviceObject&lt;/strong&gt;](wdm-pnpsamedeviceobject.md)"><strong>PnpSameDeviceObject</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpsamedeviceobject.md" data-raw-source="[&lt;strong&gt;PnpSameDeviceObject&lt;/strong&gt;](wdm-pnpsamedeviceobject.md)"><strong>PnpSameDeviceObject</strong></a>ルールは、有効なターゲットデバイスオブジェクトへのポインターを使用して、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)"><strong>Ioattachdevicetodevicestack</strong></a>を呼び出すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-targetrelationneedsref.md" data-raw-source="[&lt;strong&gt;TargetRelationNeedsRef&lt;/strong&gt;](wdm-targetrelationneedsref.md)"><strong>TargetRelationNeedsRef</strong></a></p></td>
<td align="left"><p><a href="wdm-targetrelationneedsref.md" data-raw-source="[&lt;strong&gt;TargetRelationNeedsRef&lt;/strong&gt;](wdm-targetrelationneedsref.md)"><strong>TargetRelationNeedsRef</strong></a>ルールは、 <em>TargetDeviceRelation</em>クエリを処理するときに、ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;strong&gt;DispatchPnP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><strong>DispatchPnP</strong></a>ルーチンが、次のいずれかの関数を呼び出して子デバイスの PDO を参照することを指定します。</p>
<ul>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)"><strong>Obreferenceobject へ</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>ObReferenceObjectByHandle</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer" data-raw-source="[&lt;strong&gt;ObReferenceObjectByPointer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)"><strong>ObReferenceObjectByPointer</strong></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](wdm-zwregistrycreate.md)"><strong>ZwRegistryCreate</strong></a></p></td>
<td align="left"><p><a href="wdm-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](wdm-zwregistrycreate.md)"><strong>Zwregistrycreate</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)"><strong>ZwCreateKey</strong></a>を呼び出した後に、ドライバーがレジストリキーへの開いているハンドル (つまり、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)"><strong>Zwclose</strong></a>または zwregistrycreate を呼び出す前) を保持している場合にのみ、次のレジストリ関数を呼び出すことができることを指定します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)"></a>レジストリキーのハンドルを閉じる、または削除するには、次の操作を行います。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](wdm-zwregistryopen.md)"><strong>ZwRegistryOpen</strong></a></p></td>
<td align="left"><p><a href="storport-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](storport-zwregistryopen.md)"><strong>Zwregistryopen</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)"><strong>Zwregistryopen</strong></a>を呼び出した後で、次のレジストリ関数を呼び出します。このとき、レジストリキーを開くハンドル (つまり、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)"><strong>Zwclose</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)"><strong>zwregistryopen</strong></a>を呼び出す前) を保持していることを指定します。</p></td>
</tr>
</tbody>
</table>

 

**その他のルールセットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[その他]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを使用して、**その他の sdv**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Miscellaneous.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





