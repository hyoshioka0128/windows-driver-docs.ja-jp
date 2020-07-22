---
title: ドライバーまたはライブラリが静的ドライバー検証ツールでサポートされているかどうかの判定
description: 静的ドライバー検証ツール (SDV) は、WDM、KMDF、NDIS、および Storport のドライバーとライブラリをサポートできます。 ドライバーまたはライブラリがサポートされ、正しく構成されているかどうかを判断するには、このセクションで説明する要件を参照してください。
ms.assetid: 29E93E9E-7F87-4706-97AD-DB9A32EDD388
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: d5288a967f39f8b02cd446704dcde08b10f72513
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873819"
---
# <a name="determining-if-static-driver-verifier-supports-your-driver-or-library"></a>ドライバーまたはライブラリが静的ドライバー検証ツールでサポートされているかどうかの判定

静的ドライバー検証ツール (SDV) は、WDM、KMDF、NDIS、および Storport のドライバーとライブラリを完全にサポートしており、他のドライバーは制限付きでサポートされています。 ドライバーまたはライブラリがサポートされ、正しく構成されているかどうかを判断するには、このセクションで説明する要件を参照してください。

## <a name="driver-or-library-requirements"></a>ドライバーまたはライブラリの要件

ドライバーまたはライブラリが次のいずれか**の条件を満たし、** [以下に示すクラスフレームワークライブラリ](#class-framework-libraries)にリンクしていない場合は、sdv 分析ツールですべてのルールを実行できます。

- WDM ドライバーまたはライブラリがあります。
- WdfLdr または WdfDriverEntry にリンクするドライバーまたはライブラリがあります。
- このドライバーまたはライブラリを使用して、NDIS .lib にリンクしています。
- Storport にリンクするドライバーまたはライブラリがある。

上記の条件に該当しないドライバーがある場合、SDV はドライバー "generic" を考慮して、限られたチェックのセットを実行します。

また、SDV によって検証されるライブラリは、一般的な C や C++ のライブラリではなく、カーネルモードのドライバーライブラリである必要があることに注意してください。  

静的ドライバーの検証ツールは、ドライバーまたはライブラリが複数の[ユーティリティライブラリ](#utility-libraries)にリンクされている場合でも、これらの条件を渡すドライバーまたはライブラリをサポートします。

さらに、この分析を実行するには、SDV に次のものが必要です。

- ドライバーは、[関数ロールの種類の宣言を使用して](using-function-role-type-declarations.md)、少なくとも1つのエントリポイントを宣言しました。
- ドライバーは、(MSBuild を使用した Visual Studio で) 正しくビルドおよびリンクされます。
- ドライバーまたはライブラリで KMDF が使用されている場合、ドライバーまたはライブラリは KMDF バージョン1.7 以降を使用します。
- ドライバーまたはライブラリが NDIS を使用する場合は、NDIS バージョン6.0、6.1、6.20、6.30、または6.40 が使用されます。 この一覧は変更される可能性があることに注意してください。
- ドライバーモデル (KMDF と WDM、KMDF、NDIS など) は組み合わせられません。

静的な分析結果の品質と精度に影響を与える要因が他にもあります。 その要因には次のものがあります。

- SDV によって処理されていないユーティリティライブラリの使用。
- ドライバーのサイズ (特に10万行を超えるコードがある場合)。
- 仮想関数やポインター演算など、言語固有の機能を使用します。

## <a name="visual-studio-project-requirements"></a>Visual Studio プロジェクトの要件

静的ドライバーの検証ツールを使用するには、Visual Studio プロジェクトに次の設定が必要です。

- UseDebugLibraries = false
- Platform = Win32 (x86) または x64

## <a name="class-framework-libraries"></a>クラスフレームワークライブラリ

WDM ドライバーまたはライブラリがあり、SDV を実行する場合は、ドライバーまたはライブラリが、次のいずれかのクラスフレームワークライブラリにリンクしていない必要があります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">1394</td>
<td align="left">fltMgr .lib</td>
<td align="left">rdbss</td>
<td align="left">usbrpm .lib</td>
</tr>
<tr class="even">
<td align="left">acpi .lib</td>
<td align="left">FsDepends .lib に依存します。</td>
<td align="left">RNDISMP</td>
<td align="left">videoprt</td>
</tr>
<tr class="odd">
<td align="left">armppm .lib</td>
<td align="left">fwpkclnt</td>
<td align="left">RNDISMP6</td>
<td align="left">vwififlt</td>
</tr>
<tr class="even">
<td align="left">ataport</td>
<td align="left">hidclass</td>
<td align="left">RNDISMPX</td>
<td align="left">ウォッチドッグ</td>
</tr>
<tr class="odd">
<td align="left">ath_hwpci .lib</td>
<td align="left">hidparse .lib</td>
<td align="left">rpcxdr .lib</td>
<td align="left">win32k. .lib</td>
</tr>
<tr class="even">
<td align="left">この .lib</td>
<td align="left">hwpolicy</td>
<td align="left">Saha .lib</td>
<td align="left">winhv</td>
</tr>
<tr class="odd">
<td align="left">battc</td>
<td align="left">ipmidrv_hrmcust .lib</td>
<td align="left">scsiport</td>
<td align="left">WMBBCLASS .lib</td>
</tr>
<tr class="even">
<td align="left">BdaSup</td>
<td align="left">irt30.sys 開け</td>
<td align="left">smclib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">bdl .lib</td>
<td align="left">irt30.sys 開け</td>
<td align="left">Soft1667FaultInjectionLimpetPool</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">btampm</td>
<td align="left">ks .lib</td>
<td align="left">ソフト Fckernel .lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">bthport .lib</td>
<td align="left">ksecdd .lib</td>
<td align="left">SoftFCLimpetPool</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">BTHPRINT .lib</td>
<td align="left">ksmartcpu .lib</td>
<td align="left">SoftSATAKernel .lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">classpnp</td>
<td align="left">mcd</td>
<td align="left">SoftStorageLimpetPool</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">clfs</td>
<td align="left">mpio .lib</td>
<td align="left">srvnet</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">cng</td>
<td align="left">mrxsmb</td>
<td align="left">storvsp .lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">crashdmp</td>
<td align="left">msnfsflt</td>
<td align="left">stream .lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">csr_vfp_avdtp .lib</td>
<td align="left">msrpc .lib</td>
<td align="left">tape .lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">diskdump .lib</td>
<td align="left">mup.sys</td>
<td align="left">tb .lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">drmk .lib</td>
<td align="left">ndistapi .lib</td>
<td align="left">tcpip.sys</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dumpata</td>
<td align="left">netio</td>
<td align="left">tdi. .lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dumpfve</td>
<td align="left">ntasn1k</td>
<td align="left">termdd.sys</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dxapi .lib</td>
<td align="left">parallel .lib</td>
<td align="left">USBCAMD</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dxg .lib</td>
<td align="left">pciidex</td>
<td align="left">USBCAMD2</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dxgkrnl</td>
<td align="left">portcls</td>
<td align="left">usbd</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dxgmms1</td>
<td align="left">protogon</td>
<td align="left">usbport</td>
<td align="left"></td>
</tr>
</tbody>
</table>

## <a name="utility-libraries"></a>ユーティリティライブラリ

静的ドライバーの検証ツールは、ドライバーまたはライブラリがドライバーまたはライブラリの[要件](#driver-or-library-requirements)に準拠している場合に、複数のユーティリティライブラリへのリンクを持つドライバーまたはライブラリをサポートします。

| ファイル名           |
|---------------------|
| BufferOverflowK |
| hal.dll             |
| ntoskrnl.exe        |
| 、ntstrsafe.h       |
| rtlver .lib          |
| sehupd          |
| wdm. .lib             |
| wmb .lib          |
| wdmsec .lib          |

## <a name="static-driver-verifier-and-microsoft-class-framework-libraries"></a>静的ドライバー検証ツールと Microsoft クラスフレームワークライブラリ

[クラスフレームワークライブラリ](#class-framework-libraries)の一覧でクラスフレームワークライブラリにリンクする必要がある WDM ドライバーを使用している場合は、ドライバーが静的ドライバーの検証ツールの状態に失敗します。 ただし、ある程度の静的検証を実行する[Nullcheck 規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/nullcheck)など、いくつかの汎用的な規則があります。
