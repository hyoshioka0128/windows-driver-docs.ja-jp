---
title: 印刷パイプライン プロパティ バッグ
description: 印刷パイプラインのプロパティバッグは、フィルターパイプラインのフィルター間で情報を渡すために使用されます。プロパティ nameSymbolic nameProperty typeDescriptionPrinterNameXPS\_FP\_プリンター\_NAMEVT\_、プリンター名を指定します。進捗状況 Reportxps\_FP\_進行状況\_REPORTVT\_UNKNOWNA ポインターを IUnknown インターフェイスにポインターします。 QueryInterface を呼び出して、Iprintpipelineの進捗レポートインターフェイスへのポインターを取得します。PrinterHandleXPS\_FP\_プリンター\_、VT\_BYREFThe プリンターハンドルを処理します。 フィルターは、このハンドルを閉じることはできません。PerUserPrintTicketXPS\_FP\_ユーザー\_PRINT\_TICKETVT\_UNKNOWNA pointer to IUnknown interface. QueryInterface を呼び出して、IPrintReadStreamFactory インターフェイスへのポインターを取得します。UserSecurityTokenXPS\_FP\_ユーザー\_TOKENVT\_BYREFA ハンドルは、印刷ジョブを送信したユーザーアカウントの権限を借用するために使用できます。PrintJobIdXPS\_FP\_ジョブ\_IDVT\_UI4The 印刷ジョブの識別番号。PrintClassFactoryXPS\_FP\_PRINT\_クラス\_FACTORYVT\_UNKNOWNA ポインターを IUnknown インターフェイスにします。 QueryInterface を呼び出して、IPrintClassObjectFactory インターフェイスへのポインターを取得します。IPrintCoreHelper (このプロパティ名にはシンボル名がありません)VT\_UNKNOWNA IUnknown インターフェイスへのポインター。 QueryInterface を呼び出して、IPrintCoreHelper インターフェイスへのポインターを取得します。このプロパティは、unidrvui を構成 UI DLL として使用する XPSDrv プリンタードライバーでのみ使用できます。PrintDeviceCapabilitiesXPS\_FP\_PRINTDEVICECAPABILITIES VT\_UNKNOWNA IUnknown インターフェイスへのポインター。 QueryInterface を呼び出して、IPrintReadStreamFactory インターフェイスへのポインターを取得します。XPS レンダリングフィルターで印刷フィルターパイプラインプロパティバッグから PrintDeviceCapabilities XML ファイルを取得できるようにします。
MS-HAID:
- filterpipeline\_f3fbd165-3f72-41cc-91b8-aa8b36823da9.xml
- print.print\_pipeline\_property\_bag
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 5a0fb200-a2c2-41f0-8dcf-6eb3361c148e
keywords:
- パイプラインプロパティバッグ印刷デバイスの印刷
topic_type:
- apiref
api_name:
- Print Pipeline Property Bag
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 594163978ec16ae2e95526e2647e2e4662848e7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842344"
---
# <a name="print-pipeline-property-bag"></a>印刷パイプライン プロパティ バッグ

印刷パイプラインのプロパティバッグは、フィルターパイプラインのフィルター間で情報を渡すために使用されます。

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
<td><p>PrinterName</p></td>
<td><p>XPS_FP_PRINTER_NAME</p></td>
<td><p>VT_BSTR</p></td>
<td><p>プリンター名。</p></td>
</tr>
<tr class="even">
<td><p>進行レポート</p></td>
<td><p>XPS_FP_PROGRESS_REPORT</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p><strong>IUnknown</strong>インターフェイスへのポインター。 <strong>QueryInterface</strong>を呼び出して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelineprogressreport" data-raw-source="[IPrintPipelineProgressReport](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelineprogressreport)">iprintpipelineの進捗レポート</a>インターフェイスへのポインターを取得します。</p></td>
</tr>
<tr class="odd">
<td><p>プリンターハンドル</p></td>
<td><p>XPS_FP_PRINTER_HANDLE</p></td>
<td><p>VT_BYREF</p></td>
<td><p>プリンターハンドル。 フィルターは、このハンドルを閉じることはできません。</p></td>
</tr>
<tr class="even">
<td><p>PerUserPrintTicket</p></td>
<td><p>XPS_FP_USER_PRINT_TICKET</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p><strong>IUnknown</strong>インターフェイスへのポインター。 <strong>QueryInterface</strong>を呼び出して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory" data-raw-source="[IPrintReadStreamFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory)">Iprintreadstreamfactory</a>インターフェイスへのポインターを取得します。</p></td>
</tr>
<tr class="odd">
<td><p>UserSecurityToken</p></td>
<td><p>XPS_FP_USER_TOKEN</p></td>
<td><p>VT_BYREF</p></td>
<td><p>印刷ジョブを送信したユーザーアカウントの権限を借用するためにフィルターが使用できるハンドル。</p></td>
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
<td><p><strong>IUnknown</strong>インターフェイスへのポインター。 <strong>QueryInterface</strong>を呼び出して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintclassobjectfactory" data-raw-source="[IPrintClassObjectFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintclassobjectfactory)">IPrintClassObjectFactory</a>インターフェイスへのポインターを取得します。</p></td>
</tr>
<tr class="even">
<td><p>IPrintCoreHelper</p></td>
<td><p>(このプロパティ名にはシンボル名がありません)。</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p><strong>IUnknown</strong>インターフェイスへのポインター。 <strong>QueryInterface</strong>を呼び出して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper" data-raw-source="[IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)">Iprintcorehelper</a>インターフェイスへのポインターを取得します。</p>
<p>このプロパティは、unidrvui を構成 UI DLL として使用する XPSDrv プリンタードライバーでのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>PrintDeviceCapabilities</p></td>
<td><p>XPS_FP_PRINTDEVICECAPABILITIES</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p><strong>IUnknown</strong>インターフェイスへのポインター。 <strong>QueryInterface</strong>を呼び出して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory" data-raw-source="[IPrintReadStreamFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory)">Iprintreadstreamfactory</a>インターフェイスへのポインターを取得します。</p>
<p>XPS レンダリングフィルターで印刷フィルターパイプラインプロパティバッグから PrintDeviceCapabilities XML ファイルを取得できるようにします。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[V4 プリンタードライバーのプロパティバッグ](https://docs.microsoft.com/windows-hardware/drivers/print/v4-driver-property-bags)
