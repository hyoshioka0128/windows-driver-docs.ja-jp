---
title: VirtualStorport ルール セット (Storport)
description: これらの規則を使用するには、ドライバーが Storport ミニポート (VMiniport) を仮想ドライバーへの特定の関心のある Ddi を正しく呼び出すことを確認します。
ms.assetid: 7223AFF1-7EB7-4E25-BC50-8A7BF4E4BE59
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5fbae0cfeb9a8cd01da05ea1ad8b8a2fa489335f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536799"
---
# <a name="virtualstorport-rule-set-storport"></a>VirtualStorport ルール セット (Storport)


これらの規則を使用するには、ドライバーが Storport ミニポート (VMiniport) を仮想ドライバーへの特定の関心のある Ddi を正しく呼び出すことを確認します。

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
<td align="left"><p><a href="storport-doubleexfreepool.md" data-raw-source="[&lt;strong&gt;DoubleExFreePool&lt;/strong&gt;](storport-doubleexfreepool.md)"><strong>DoubleExFreePool</strong></a></p></td>
<td align="left"><p>このルールは、ドライバーが同じプール メモリのブロックを 2 回解放を試行しないことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-doublekesetevent.md" data-raw-source="[&lt;strong&gt;DoubleKeSetEvent&lt;/strong&gt;](storport-doublekesetevent.md)"><strong>DoubleKeSetEvent</strong></a></p></td>
<td align="left"><p>このルールはことを確認します<strong>KeSetEvent</strong>同じイベント オブジェクトに対して 2 回は呼び出されません。 同じイベント オブジェクトがルーチンに渡された場合、ドライバーによってルールが失敗します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-iofreeirp.md" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](storport-iofreeirp.md)"><strong>IoFreeIrp</strong></a></p></td>
<td align="left"><p>このルールは、ことを確認で割り当てられた IRP <strong>IoAllocateIrp</strong>によって解放されるか<strong>IoFreeIrp</strong>その完了ルーチンは設定を取得または<strong>IoSetCompletionRoutine</strong>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportvirtualdevice.md" data-raw-source="[&lt;strong&gt;StorPortVirtualDevice&lt;/strong&gt;](storport-storportvirtualdevice.md)"><strong>StorPortVirtualDevice</strong></a></p></td>
<td align="left"><p>終了時にこの規則を確認、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff557390" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557390)"> <strong>HwStorFindAdapter</strong> </a> 、ルーチン、 <strong>VirtualDevice</strong>フィールドに、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563901" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563901)"> <strong>PORT_CONFIGURATION_INFORMATION (Storport)</strong> </a>構造に設定されている<strong>FALSE</strong>します。 ルールは、物理 StorPort ミニポートにのみ適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportvirtualdevice2.md" data-raw-source="[&lt;strong&gt;StorPortVirtualDevice2&lt;/strong&gt;](storport-storportvirtualdevice2.md)"><strong>StorPortVirtualDevice2</strong></a></p></td>
<td align="left"><p>終了時にこの規則を確認、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff557390" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557390)"> <strong>HwStorFindAdapter</strong> </a> 、ルーチン、 <strong>VirtualDevice</strong>フィールドに、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563901" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563901)"> <strong>PORT_CONFIGURATION_INFORMATION (Storport)</strong> </a>構造に設定されている<strong>TRUE</strong>します。 ルールは、仮想 StorPort ミニポートにのみ適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](storport-withincriticalregion.md)"><strong>WithinCriticalRegion</strong></a></p></td>
<td align="left"><p>このルールを検証するドライバー&#39;s を呼び出す通常カーネル APC 配信が無効になっている場合にのみ、同期機能が加えられたに特定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](storport-zwregistrycreate.md)"><strong>ZwRegistryCreate</strong></a></p></td>
<td align="left"><p>このルールは、のレジストリ キーを識別するハンドルが作成されたことを確認します。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566425" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566425)"> <strong>ZwCreateKey</strong> </a>他で正しく使用されて、その後<em>ZwXxx</em>ルーチン。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567014" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567014)"> <strong>ZwOpenKey</strong> </a>ルーチンは、既に開いているハンドルを呼び出さないでください。 ルーチン<a href="https://msdn.microsoft.com/library/windows/hardware/ff566447" data-raw-source="[&lt;strong&gt;ZwEnumerateKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566447)"> <strong>ZwEnumerateKey</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566453" data-raw-source="[&lt;strong&gt;ZwEnumerateValueKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566453)"> <strong>ZwEnumerateValueKey</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566457" data-raw-source="[&lt;strong&gt;ZwFlushKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566457)"> <strong>ZwFlushKey</strong> </a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567060" data-raw-source="[&lt;strong&gt;ZwQueryKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567060)"> <strong>ZwQueryKey</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567069" data-raw-source="[&lt;strong&gt;ZwQueryValueKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567069)"> <strong>ZwQueryValueKey</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567109" data-raw-source="[&lt;strong&gt;ZwSetValueKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567109)"> <strong>ZwSetValueKey</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566417" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566417)"> <strong>ZwClose</strong></a>、および<a href="https://msdn.microsoft.com/library/windows/hardware/ff566437" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566437)"> <strong>ZwDeleteKey</strong> </a>でないと呼ばれる必要があります、その処理&#39;t を開きます。 返す前にハンドルを閉じてもする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](storport-zwregistryopen.md)"><strong>ZwRegistryOpen</strong></a></p></td>
<td align="left"><p>このルールを使用して、レジストリ キーを識別するハンドルを開いたことを確認します。 <strong>ZwOpenKey</strong>他 ZwXxx ルーチンで正しく使用されて、その後です。 ルーチン<strong>ZwEnumerateKey</strong>、 <strong>ZwEnumerateValueKey</strong>、 <strong>ZwFlushKey</strong>、 <strong>ZwQueryKey</strong>、 <strong>ZwQueryValueKey</strong>、 <strong>ZwSetValueKey</strong>、 <strong>ZwClose</strong>、および<strong>ZwDeleteKey</strong>呼び出さないでくださいハンドルでは&#39;t を開きます。 返す前にハンドルを閉じてもする必要があります。</p></td>
</tr>
</tbody>
</table>

 

**VirtualStorport ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています.**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **VirtualStorport**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **VirtualStorport.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:VirtualStorport.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 





