---
title: ドライバーまたはライブラリが静的ドライバー検証ツールでサポートされているかどうかの判定
description: Static Driver Verifier (SDV) は、WDM、KMDF、NDIS、および Storport のドライバーとライブラリをサポートできます。 調べるには、ドライバーまたはライブラリがサポートされていて正しく構成されているかどうか、このセクションで説明されている要件を参照してください。
ms.assetid: 29E93E9E-7F87-4706-97AD-DB9A32EDD388
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fe67c93afa12172b53cca50763f77eb2f3d6f87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382980"
---
# <a name="determining-if-static-driver-verifier-supports-your-driver-or-library"></a>ドライバーまたはライブラリが静的ドライバー検証ツールでサポートされているかどうかの判定


Static Driver Verifier (SDV) は完全に WDM、KMDF、NDIS、および Storport のドライバーとライブラリをサポートし、その他のドライバーのサポートが限られています。 調べるには、ドライバーまたはライブラリがサポートされていて正しく構成されているかどうか、このセクションで説明されている要件を参照してください。

## <a name="driver-or-library-requirements"></a>ドライバーまたはライブラリの要件


ドライバーまたはライブラリは次の条件のいずれかを満たす場合は、SDV の分析ツールでルールの完全なセットを実行できます。

-   WDM ドライバーやライブラリがあるし、ドライバーまたはライブラリがクラスのフレームワーク (Microsoft 提供のライブラリ) にリンクされません。 詳細については、次を参照してください。[クラス フレームワーク ライブラリ](#class-framework-libraries)します。
-   ある、ドライバーやライブラリ WdfLdr.lib または WdfDriverEntry.lib にリンクします。
-   ある、ドライバーやライブラリ NDIS.lib にリンクします。
-   ある、ドライバーやライブラリ Storport.lib にリンクします。

Static Driver Verifier は、ドライバーまたはドライバーまたはライブラリが複数にリンクする場合でも、これらの条件を通過するライブラリをサポートしています。[ユーティリティ ライブラリ](#utility-libraries)します。

さらに、分析を実行するには、SDV いる必要があります。

-   ドライバーには、少なくとも 1 つのエントリ ポイントが宣言されている[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。
-   ドライバーは、ビルドし、正しく (Visual Studio は MSBuild を使用して) にリンクします。
-   ドライバーまたはライブラリは、KMDF を使用している場合、ドライバーまたはライブラリ KDMF バージョン 1.7 以降を使用します。
-   ドライバーまたはライブラリは、NDIS を使用している場合は、NDIS version 6.0、6.1、6.20、6.30、または 6.40 が使用されます。 この一覧は変更されることに注意してください。
-   ドライバーはドライバー モデル (と WDM、KMDF または KMDF、NDIS) を結合していません。

品質と静的分析結果の精度に影響するその他の要素があります。 これらの要因は次のとおりです。

-   SDV で処理されていないユーティリティ ライブラリを使用します。
-   100 を超える K 行のコードがある場合は特に、ドライバーのサイズ。
-   仮想関数ポインターの算術演算などの言語固有の機能を使用します。

## <a name="visual-studio-project-requirements"></a>Visual Studio プロジェクトの要件


Static Driver Verifier を使用するには、Visual Studio プロジェクトは、次の設定が必要です。

-   UseDebugLibraries = false
-   プラットフォーム (x86) Win32 または x64 を =

## <a name="class-framework-libraries"></a>Framework のクラス ライブラリ


WDM ドライバーまたはライブラリがある、SDV を実行する場合は、ドライバーまたはライブラリする必要があります、次のクラスのフレームワーク ライブラリのいずれかにリンクしません。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">1394bus.lib</td>
<td align="left">FltMgr.lib</td>
<td align="left">rdbss.lib</td>
<td align="left">usbrpm.lib</td>
</tr>
<tr class="even">
<td align="left">acpi.lib</td>
<td align="left">FsDepends.lib</td>
<td align="left">RNDISMP.lib</td>
<td align="left">videoprt.lib</td>
</tr>
<tr class="odd">
<td align="left">armppm.lib</td>
<td align="left">fwpkclnt.lib</td>
<td align="left">RNDISMP6.lib</td>
<td align="left">vwififlt.lib</td>
</tr>
<tr class="even">
<td align="left">ataport.lib</td>
<td align="left">hidclass.lib</td>
<td align="left">RNDISMPX.lib</td>
<td align="left">watchdog.lib</td>
</tr>
<tr class="odd">
<td align="left">ath_hwpci.lib</td>
<td align="left">hidparse.lib</td>
<td align="left">rpcxdr.lib</td>
<td align="left">win32k.lib</td>
</tr>
<tr class="even">
<td align="left">athhal.lib</td>
<td align="left">hwpolicy.lib</td>
<td align="left">Saha.lib</td>
<td align="left">winhv.lib</td>
</tr>
<tr class="odd">
<td align="left">battc.lib</td>
<td align="left">ipmidrv_hrmcust.lib</td>
<td align="left">scsiport.lib</td>
<td align="left">WMBBCLASS.lib</td>
</tr>
<tr class="even">
<td align="left">BdaSup.lib</td>
<td align="left">irt30.lib</td>
<td align="left">smclib.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">bdl.lib</td>
<td align="left">irt30.lib</td>
<td align="left">Soft1667FaultInjectionLimpetPool.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">btampm.lib</td>
<td align="left">ks.lib</td>
<td align="left">SoftFCKernel.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">bthport.lib</td>
<td align="left">ksecdd.lib</td>
<td align="left">SoftFCLimpetPool.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">BTHPRINT.lib</td>
<td align="left">ksmartcpu.lib</td>
<td align="left">SoftSATAKernel.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">classpnp.lib</td>
<td align="left">mcd.lib</td>
<td align="left">SoftStorageLimpetPool.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">clfs.lib</td>
<td align="left">mpio.lib</td>
<td align="left">srvnet.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">cng.lib</td>
<td align="left">mrxsmb.lib</td>
<td align="left">storvsp.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">crashdmp.lib</td>
<td align="left">msnfsflt.lib</td>
<td align="left">stream.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">csr_vfp_avdtp.lib</td>
<td align="left">msrpc.lib</td>
<td align="left">tape.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">diskdump.lib</td>
<td align="left">mup.lib</td>
<td align="left">tbs.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">drmk.lib</td>
<td align="left">ndistapi.lib</td>
<td align="left">tcpip.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dumpata.lib</td>
<td align="left">netio.lib</td>
<td align="left">tdi.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dumpfve.lib</td>
<td align="left">ntasn1k.lib</td>
<td align="left">termdd.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dxapi.lib</td>
<td align="left">parallel.lib</td>
<td align="left">USBCAMD.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dxg.lib</td>
<td align="left">pciidex.lib</td>
<td align="left">USBCAMD2.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dxgkrnl.lib</td>
<td align="left">portcls.lib</td>
<td align="left">usbd.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dxgmms1.lib</td>
<td align="left">protogon.lib</td>
<td align="left">usbport.lib</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="utility-libraries"></a>ユーティリティ ライブラリ


Static Driver Verifier は、ドライバーまたはドライバーまたはライブラリに準拠している場合は、複数のユーティリティ ライブラリにリンクをされているライブラリをサポートしています、[ドライバーまたはライブラリの要件](#driver-or-library-requirements)します。

|                     |
|---------------------|
| BufferOverflowK.lib |
| hal.lib             |
| ntoskrnl.lib        |
| ntstrsafe.lib       |
| rtlver.lib          |
| sehupd.lib          |
| wdm.lib             |
| wmilib.lib          |
| wdmsec.lib          |

 

 

 





