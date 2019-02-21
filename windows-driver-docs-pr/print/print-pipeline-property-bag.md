---
title: パイプラインのプロパティ バッグを印刷します。
description: 印刷のパイプラインのプロパティ バッグを使用して、フィルター パイプライン内のフィルターの間で情報を渡します。プロパティ nameSymbolic nameProperty typeDescriptionPrinterNameXPS\_FP\_プリンター\_NAMEVT\_BSTRThe プリンターの名前。ProgressReportXPS\_FP\_進行状況\_REPORTVT\_UNKNOWNA IUnknown インターフェイス ポインター。 IPrintPipelineProgressReport インターフェイスへのポインターを取得する QueryInterface を呼び出します。PrinterHandleXPS\_FP\_プリンター\_ハンドル VT\_BYREFThe プリンター ハンドル。 フィルターは、このハンドルを閉じないでください。PerUserPrintTicketXPS\_FP\_ユーザー\_印刷\_TICKETVT\_UNKNOWNA IUnknown インターフェイス ポインター。 IPrintReadStreamFactory インターフェイスへのポインターを取得する QueryInterface を呼び出します。UserSecurityTokenXPS\_FP\_ユーザー\_TOKENVT\_BYREFA 処理、フィルターは、印刷ジョブを送信するユーザー アカウントの借用を使用できます。PrintJobIdXPS\_FP\_ジョブ\_IDVT\_UI4The 印刷ジョブの識別番号。PrintClassFactoryXPS\_FP\_印刷\_クラス\_FACTORYVT\_UNKNOWNA IUnknown インターフェイス ポインター。 IPrintClassObjectFactory インターフェイスへのポインターを取得する QueryInterface を呼び出します。IPrintCoreHelper (このプロパティ名のシンボリック名がありません)。VT\_UNKNOWNA IUnknown インターフェイス ポインター。 IPrintCoreHelper インターフェイスへのポインターを取得する QueryInterface を呼び出します。このプロパティは構成 UI の DLL として、unidrvui.dll を使用する XPSDrv プリンター ドライバーで利用できるのみことに注意してください。PrintDeviceCapabilitiesXPS\_FP\_PRINTDEVICECAPABILITIES VT\_UNKNOWNA IUnknown インターフェイス ポインター。 IPrintReadStreamFactory インターフェイスへのポインターを取得する QueryInterface を呼び出します。印刷フィルター パイプラインのプロパティ バッグから PrintDeviceCapabilities XML ファイルを取得する XPS レンダリング フィルターを使用できます。
MS-HAID:
- filterpipeline\_f3fbd165-3f72-41cc-91b8-aa8b36823da9.xml
- print.print\_pipeline\_property\_bag
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 5a0fb200-a2c2-41f0-8dcf-6eb3361c148e
keywords:
- パイプラインのプロパティ バッグの印刷デバイスを印刷します。
topic_type:
- apiref
api_name:
- Print Pipeline Property Bag
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23ae404f052d7ea69152dacfcf9203fde5c9679f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550786"
---
# <a name="print-pipeline-property-bag"></a>パイプラインのプロパティ バッグを印刷します。

印刷のパイプラインのプロパティ バッグを使用して、フィルター パイプライン内のフィルターの間で情報を渡します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ名</th>
<th>シンボリック名</th>
<th>プロパティの型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>プリンター名</p></td>
<td><p>XPS_FP_PRINTER_NAME</p></td>
<td><p>VT_BSTR</p></td>
<td><p>プリンターの名前。</p></td>
</tr>
<tr class="even">
<td><p>ProgressReport</p></td>
<td><p>XPS_FP_PROGRESS_REPORT</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>ポインター、 <strong>IUnknown</strong>インターフェイス。 呼び出す<strong>QueryInterface</strong>へのポインターを取得する、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff554314" data-raw-source="[IPrintPipelineProgressReport](https://msdn.microsoft.com/library/windows/hardware/ff554314)">IPrintPipelineProgressReport</a>インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>PrinterHandle</p></td>
<td><p>XPS_FP_PRINTER_HANDLE</p></td>
<td><p>VT_BYREF</p></td>
<td><p>プリンター ハンドル。 フィルターは、このハンドルを閉じないでください。</p></td>
</tr>
<tr class="even">
<td><p>PerUserPrintTicket</p></td>
<td><p>XPS_FP_USER_PRINT_TICKET</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>ポインター、 <strong>IUnknown</strong>インターフェイス。 呼び出す<strong>QueryInterface</strong>へのポインターを取得する、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff554338" data-raw-source="[IPrintReadStreamFactory](https://msdn.microsoft.com/library/windows/hardware/ff554338)">IPrintReadStreamFactory</a>インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p>UserSecurityToken</p></td>
<td><p>XPS_FP_USER_TOKEN</p></td>
<td><p>VT_BYREF</p></td>
<td><p>フィルターは、印刷ジョブを送信するユーザー アカウントの借用を使用できるハンドル。</p></td>
</tr>
<tr class="even">
<td><p>PrintJobId</p></td>
<td><p>XPS_FP_JOB_ID</p></td>
<td><p>VT_UI4</p></td>
<td><p>印刷ジョブの識別番号。</p></td>
</tr>
<tr class="odd">
<td><p>PrintClassFactory</p></td>
<td><p>XPS_FP_PRINT_CLASS_FACTORY</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>ポインター、 <strong>IUnknown</strong>インターフェイス。 呼び出す<strong>QueryInterface</strong>へのポインターを取得する、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551955" data-raw-source="[IPrintClassObjectFactory](https://msdn.microsoft.com/library/windows/hardware/ff551955)">IPrintClassObjectFactory</a>インターフェイス。</p></td>
</tr>
<tr class="even">
<td><p>IPrintCoreHelper</p></td>
<td><p>(このプロパティ名のシンボリック名がありません) です。</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>ポインター、 <strong>IUnknown</strong>インターフェイス。 呼び出す<strong>QueryInterface</strong>へのポインターを取得する、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552960" data-raw-source="[IPrintCoreHelper](https://msdn.microsoft.com/library/windows/hardware/ff552960)">IPrintCoreHelper</a>インターフェイス。</p>
<p>このプロパティは構成 UI の DLL として、unidrvui.dll を使用する XPSDrv プリンター ドライバーで利用できるのみことに注意してください。</p></td>
</tr>
<tr class="odd">
<td><p>PrintDeviceCapabilities</p></td>
<td><p>XPS_FP_PRINTDEVICECAPABILITIES</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>ポインター、 <strong>IUnknown</strong>インターフェイス。 呼び出す<strong>QueryInterface</strong>へのポインターを取得する、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff554338" data-raw-source="[IPrintReadStreamFactory](https://msdn.microsoft.com/library/windows/hardware/ff554338)">IPrintReadStreamFactory</a>インターフェイス。</p>
<p>印刷フィルター パイプラインのプロパティ バッグから PrintDeviceCapabilities XML ファイルを取得する XPS レンダリング フィルターを使用できます。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[V4 プリンター ドライバーのプロパティ バッグ](https://docs.microsoft.com/windows-hardware/drivers/print/v4-driver-property-bags)
