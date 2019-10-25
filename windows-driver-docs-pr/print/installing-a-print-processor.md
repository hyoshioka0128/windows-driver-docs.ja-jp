---
title: 印刷プロセッサをインストールする
description: 印刷プロセッサをインストールする
ms.assetid: 4e9e1148-16a3-42f6-a262-1eef014636d0
keywords:
- プリントプロセッサ WDK、インストール
- プリントプロセッサ WDK のインストール
- 印刷キュー WDK、プリントプロセッサのインストール
- プリントプロセッサと印刷キュー WDK の関連付け
- プリントプロセッサ WDK、関連付けられる印刷キュー
- 印刷キュー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 024fadaef3fef6d144eec8ce8fe2e73affad7f33
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843625"
---
# <a name="installing-a-print-processor"></a>印刷プロセッサをインストールする





印刷プロセッサをインストールするには、インストールアプリケーションでスプーラの**Addprintprocessor**関数を呼び出す必要があります。 印刷プロセッサを印刷キューに関連付けるには、PrintProcessor エントリの INF ファイルでそのファイル名を一覧表示します。 このエントリは、プリントプロセッサが関連付けられるすべての印刷キューに含める必要があります。 詳細については、「[プリンター INF ファイル](printer-inf-files.md)」を参照してください。

インストールアプリケーションでスプーラの**Addprinter**関数が呼び出され、プリンター\_INFO\_2 の構造体が入力引数として使用されている場合は、(INF ファイルから取得した) 印刷プロセッサ名を構造体メンバーとして指定します。 ( **Addprintprocessor**および**addprinter**の関数とプリンター\_INFO\_2 の構造については、Microsoft Windows SDK のドキュメントを参照してください。)

### <a name="associating-a-print-processor-with-a-pnp-installed-print-queue"></a>印刷プロセッサと PnP がインストールされた印刷キューの関連付け

プラグアンドプレイ (PnP) マネージャーが、Windows 2000 または Windows XP を実行しているシステムに印刷キューを検出してインストールし、印刷キューをインストールするために使用される INF ファイルに既定の Windows プリントプロセッサ以外の PrintProcessor エントリが含まれている場合は、WinPrintでは、プリントプロセッサは印刷キューに関連付けられません。 ただし、プリントプロセッサはインストールされます。 (プリンターの追加ウィザードを使用して印刷キューをインストールした場合、印刷プロセッサは印刷キューに正しく関連付けられていることに注意してください。 また、Microsoft Windows Server 2003 以降の PnP マネージャーがプリントプロセッサを印刷キューに正しく関連付けることにも注意してください。)

Windows 2000 および Windows XP でプラグアンドプレイインストールの印刷キューにプリントプロセッサを関連付けるには、プリンタ\_イベント\_プリンタインターフェイス DLL の[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)関数に大文字/小文字を挿入します。 Microsoft Windows Server 2003 以降では、 **DrvPrinterEvent**関数に、プリンター\_イベント\_初期化ケースを追加する必要はありません。

次のコード例では、PRINTER\_INFO\_2 構造体の**Pprintprocessor**メンバーをプリントプロセッサの名前に設定し、 **setprinter**関数 (Windows SDK のドキュメントで説明) を呼び出して更新します。プリンターの設定。 *Gszprintproc*のプリントプロセッサの名前は、INF ファイル内の printprocessor エントリのものと同じであることに注意してください。

```cpp
BOOL
DrvPrinterEvent(
               LPWSTR  pPrinterName,
               INT     Event,
               DWORD   Flags,
               LPARAM  lParam
               )

{
  PRINTER_DEFAULTS  PrinterDef = {NULL, NULL, PRINTER_ALL_ACCESS};
  HANDLE            hPrinter;
  LPPRINTER_INFO_2  pInfo = NULL;
  DWORD             cbNeeded;
  TCHAR             gszPrintProc[] = TEXT("<Print processor name>");
  BOOL              bRet = TRUE;

  switch (Event)
  {
    case PRINTER_EVENT_INITIALIZE:
      if (OpenPrinter(pPrinterName, &hPrinter, &PrinterDef))
      {
        if ( !GetPrinter( hPrinter, 2, (LPBYTE) pInfo, 0, &cbNeeded ) &&
           (GetLastError() != ERROR_INSUFFICIENT_BUFFER) )
        {
          bRet = FALSE;
        }
        if (bRet == TRUE)
        {
          pInfo = (LPPRINTER_INFO_2) LocalAlloc(LPTR, cbNeeded);
          bRet = pInfo ? TRUE : FALSE;
        }
        if (bRet == TRUE)
        {
          if (GetPrinter(hPrinter, 2, (LPBYTE) pInfo, cbNeeded, &cbNeeded))
          {
            pInfo->pPrintProcessor = gszPrintProc;
            SetPrinter(hPrinter, 2, (LPBYTE) pInfo, 0);
          }
          else 
          {
            bRet = FALSE;
          }
          if (pInfo)
          {
            LocalFree(pInfo);
          }
        }
        ClosePrinter(hPrinter);
      }
      else  // OpenPrinter failed
      {
        bRet = FALSE;
      }
    break;
    // cases for other events

    default:
      break;
  }  // end switch
  return bRet;
}
```

### <a href="" id="associating-a-print-processor-with-a-print-queue-during-printer-driver"></a>プリンタードライバーのアップグレード中の印刷プロセッサと印刷キューの関連付け

プリンタードライバーが更新されても、更新された印刷キューの印刷プロセッサは変更されません。 新しいプリンタードライバーが特定の印刷プロセッサを必要とする場合、printer interface DLL の[**DrvUpgradePrinter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvupgradeprinter)関数は、プリンターの**pprintprocessor**メンバーを新しい印刷の名前に設定する必要があります。これには、printer\_INFO\_2 の構造体sp. その後、この関数は、 **Setprinter**を呼び出してプリンターの設定を更新します。 スプーラは、各プリンタに対して**DrvUpgradePrinter**関数を1回呼び出します。これにより、そのドライバを使用するすべてのプリンタも必要なプリントプロセッサを使用します。 これらの点を示すコード例を次に示します。

```cpp
BOOL
DrvUpgradePrinter(
                 DWORD   Level,
                 LPBYTE  pDriverUpgradeInfo
                 )
{
  HANDLE                  hPrinter;
  PRINTER_DEFAULTS        PrinterDef = {NULL, NULL, PRINTER_ALL_ACCESS};
 PDRIVER_UPGRADE_INFO_2  pDUI2;
  LPPRINTER_INFO_2        pInfo = NULL;
 DWORD                   cbNeeded;
  TCHAR                   gszPrintProc[]   = TEXT("<Print processor name>");
  TCHAR                   gszPrintDriver[] = TEXT("<Printer driver name>");
  BOOL                    bRet = TRUE;

  if ((Level == 2)                                            &&
      (pDUI2 = (PDRIVER_UPGRADE_INFO_2)pDriverUpgradeInfo)    &&
      (OpenPrinter(pDUI2->pPrinterName, &hPrinter, &PrinterDef)))
  {
    if ( !GetPrinter( hPrinter, 2, (LPBYTE) pInfo, 0, &cbNeeded )  &&
         (GetLastError() != ERROR_INSUFFICIENT_BUFFER) )
    {
       bRet = FALSE;
    }
    if (bRet == TRUE)
    {
      pInfo = (LPPRINTER_INFO_2) LocalAlloc(LPTR, cbNeeded);
      bRet = pInfo ? TRUE : FALSE;
    }
    if (bRet == TRUE)
    {
      if (GetPrinter(hPrinter, 2, (LPBYTE) pInfo, cbNeeded, &cbNeeded))
      {
      //
      // This function is called for every printer queue that uses a driver
      // for which one or more files were updated. However, we only want to
      // update the printer queue's "driver" by a particular driver.
      //
      if ( !lstrcmpi(pInfo->pDriverName, gszPrintDriver) )
      {
        pInfo->pPrintProcessor =  gszPrintProc;
        SetPrinter(hPrinter, 2, (LPBYTE) pInfo, 0);
      }
    else  // GetPrinter 
    {
      bRet = FALSE;
    }
    if (pInfo)
    {
      LocalFree(pInfo);
    }
    ClosePrinter(hPrinter);
  }
  else  // Level != 2 or pDUI2 == NULL or OpenPrinter failed
  {
    bRet = FALSE;
  }
  return bRet;
}
```

 

 




