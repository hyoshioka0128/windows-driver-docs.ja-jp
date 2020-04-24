---
title: Windows Driver Kit (WDK) のヘッダー ファイル
description: Windows Driver Kit (WDK) のヘッダー ファイル
ms.assetid: 7d02148d-502d-4b49-9c56-9fff498dd2af
keywords:
- ドライバー設計の決定 WDK, ヘッダー ファイルの変更
- ドライバーの設計 WDK, ヘッダー ファイルの変更
- ヘッダー ファイル WDK
- ヘッダー ファイル WDK, 変更
- .h ファイル
- ユーザー モード ヘッダー ファイル WDK
- カーネル モード ヘッダー ファイル WDK
- ファイル WDK ヘッダー ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2613202fb101bcd13bd6cbc2d76c1ab39b7766f
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72825156"
---
# <a name="header-files-in-the-windows-driver-kit"></a>Windows Driver Kit (WDK) のヘッダー ファイル


[Windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/) には、カーネル モード ドライバーとユーザー モード ドライバーをビルドする際に必要となるすべてのヘッダー ファイル (.h ファイル) が含まれています。 ヘッダー ファイルは WDK インストール フォルダー内の Include フォルダーにあります。 例:C:\\Program Files (x86)\\Windows Kits\\10\\Include

ヘッダー ファイルには、バージョン情報も含まれているため、ドライバーを実行する Windows のバージョンには関係なく、同じヘッダー ファイル セットを使用できます。

## <a name="span-idconstants_that_represent_windows_versionsspanspan-idconstants_that_represent_windows_versionsspanspan-idconstants_that_represent_windows_versionsspanconstants-that-represent-windows-versions"></a><span id="Constants_that_represent_Windows_versions"></span><span id="constants_that_represent_windows_versions"></span><span id="CONSTANTS_THAT_REPRESENT_WINDOWS_VERSIONS"></span>Windows バージョンを表す定数


WDK 中のヘッダー ファイルには、Windows オペレーティング システムの特定のバージョンでのみ利用できるプログラミング要素を指定する条件ステートメントが含まれています。 バージョン付きの要素には、関数、列挙、構造体と構造体メンバーがあります。

オペレーティング システムの各バージョンで利用可能なプログラミング要素を指定するために、ヘッダー ファイルには、NTDDI\_VERSION の値と、Sdkddkver.h で事前に定義された一連の定数値を比較するプリプロセッサの条件が記述されています。

以下に Microsoft Windows オペレーティング システムのバージョンを表す定義済みの定数値を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Constant</th>
<th align="left">オペレーティング システムのバージョン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>NTDDI_WIN10</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>NTDDI_WINBLUE</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NTDDI_WIN8</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>NTDDI_WIN7</p></td>
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NTDDI_WS08SP4</p></td>
<td align="left"><p>Windows Server 2008 SP4</p></td>
</tr>
<tr class="even">
<td align="left"><p>NTDDI_WS08SP3</p></td>
<td align="left"><p>Windows Server 2008 SP3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NTDDI_WS08SP2</p></td>
<td align="left"><p>Windows Server 2008 SP2</p></td>
</tr>
<tr class="even">
<td align="left"><p>NTDDI_WS08</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
</tbody>
</table>

 

WDK ヘッダー ファイルには、バージョン固有の DDI 要素の例が数多く記述されています。 この条件付き宣言は、Wdm.h ヘッダー ファイルにあります。このヘッダー ファイルは、カーネル モード ドライバーに含まれることがあります。

```cpp
#if (NTDDI_VERSION >= NTDDI_WIN7)
_Must_inspect_result_
NTKERNELAPI
NTSTATUS
KeSetTargetProcessorDpcEx (
    _Inout_ PKDPC Dpc,
    _In_ PPROCESSOR_NUMBER ProcNumber
    );
#endif
```

この例で、[**KeSetTargetProcessorDpcEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettargetprocessordpcex) 関数は Windows 7 とそれ以降の Windows バージョンでのみ利用できることがわかります。

この条件付き宣言は、Winspool.h ヘッダー ファイルにあります。このヘッダー ファイルは、ユーザー モード ドライバーに含まれることがあります。

```ManagedCPlusPlus
#if (NTDDI_VERSION >= NTDDI_WIN7)
...
BOOL
WINAPI
GetPrintExecutionData(
    _Out_ PRINT_EXECUTION_DATA *pData
    );

#endif // (NTDDI_VERSION >= NTDDI_WIN7)
```

この例で、[**GetPrintExecutionData**](https://docs.microsoft.com/windows/desktop/printdocs/getprintexecutiondata) 関数は Windows 7 とそれ以降の Windows バージョンでのみ利用できることがわかります。

## <a name="span-idheader_files_for_the_kernel_mode_driver_frameworkspanspan-idheader_files_for_the_kernel_mode_driver_frameworkspanspan-idheader_files_for_the_kernel_mode_driver_frameworkspanheader-files-for-the-kernel-mode-driver-framework"></a><span id="Header_files_for_the_Kernel_Mode_Driver_Framework"></span><span id="header_files_for_the_kernel_mode_driver_framework"></span><span id="HEADER_FILES_FOR_THE_KERNEL_MODE_DRIVER_FRAMEWORK"></span>カーネル モード ドライバー フレームワークのヘッダー ファイル


WDK では、複数のバージョンの Windows がサポートされており、カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) も複数のバージョンがサポートされています。 WDK ヘッダー ファイルのバージョン情報は、Windows バージョンに関するものであり、KMDF や UMDF のバージョンに関する情報ではありません。 KMDF と UMDF の異なるバージョンのヘッダー ファイルは、別のディレクトリに格納されています。

 

 





