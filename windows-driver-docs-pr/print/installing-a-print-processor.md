---
title: 印刷プロセッサをインストールする
description: 印刷プロセッサをインストールする
ms.assetid: 4e9e1148-16a3-42f6-a262-1eef014636d0
keywords:
- プリント プロセッサ、WDK をインストールします。
- プリント プロセッサ WDK をインストールします。
- 印刷キュー WDK、プロセッサのインストールの印刷
- プリント プロセッサを WDK の印刷キューに関連付ける
- プリント プロセッサ WDK、印刷キューとの関連付け
- WDK の印刷キュー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bda252290d66e281fa4172cad9ddaa7ffe1d09f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572859"
---
# <a name="installing-a-print-processor"></a>印刷プロセッサをインストールする





プリント プロセッサをインストールするには、インストール アプリケーションが、スプーラーを呼び出す必要があります**AddPrintProcessor**関数。 印刷キューにプリント プロセッサを関連付けるには、PrintProcessor エントリで、INF ファイルでは、そのファイル名を一覧表示します。 このエントリは、プリント プロセッサが関連付けられるすべての印刷キューを含める必要があります。 詳細については、次を参照してください。[プリンター INF ファイル](printer-inf-files.md)します。

インストール アプリケーションから、スプーラーの**AddPrinter**関数は、プリンターを使用して\_情報\_2 は、入力引数として構造体、プリント プロセッサを指定します (INF ファイルから取得した) の名前として、構造体のメンバー。 (、 **AddPrintProcessor**と**AddPrinter**関数とプリンター\_情報\_2 構造が、Microsoft Windows SDK ドキュメントに記載されています)。

### <a name="associating-a-print-processor-with-a-pnp-installed-print-queue"></a>プリント プロセッサを PnP-インストールされている印刷キューに関連付ける

既定の Windows がプリント プロセッサ、WinPrint である場合は、プラグ アンド プレイ (PnP) マネージャーが検出され、Windows 2000 または Windows XP では、いずれかを実行するシステムで印刷キューをインストールし、以外の印刷キューをインストールするために使用する INF ファイルに PrintProcessor エントリが含まれている場合、プリント プロセッサは、印刷キューに関連付けできません。 ただし、プリント プロセッサがインストールされます。 (プリンターの追加ウィザードを使用して、印刷キューをインストールする場合、プリント プロセッサが正しく印刷キューに関連付けられているに注意してください。 また、印刷キューをプリント プロセッサを Microsoft Windows Server 2003 以降の PnP マネージャーが正しく関連付けられていること。)

プリント プロセッサにプラグ アンド プレイのインストールを Windows 2000 および Windows XP での印刷キューに関連付けるには、プリンター\_イベント\_プリンター インターフェイスの DLL の初期化ケース[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)関数。 Microsoft Windows Server 2003 以降では、プリンターを追加する必要はありません\_イベント\_の初期化の場合、 **DrvPrinterEvent**関数。

次のコード例のセット、 **pPrintProcessor**プリンターのメンバー\_情報\_、プリント プロセッサは、呼び出し、その後の名前に 2 つの構造、 **SetPrinter**関数 (Windows SDK のドキュメントで説明)、プリンターの設定を更新します。 注意のプリント プロセッサの名前*gszPrintProc* INF ファイルの PrintProcessor エントリである必要がありますと同じです。

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

### <a href="" id="associating-a-print-processor-with-a-print-queue-during-printer-driver"></a>印刷キューとプリンター ドライバーのアップグレード中にプリント プロセッサを関連付ける

プリンター ドライバーが更新されると、更新された印刷キューのプリント プロセッサは変更されません。 新しいプリンタ ドライバには、特定のプリント プロセッサが必要とする場合、プリンターの DLL のインターフェイス[ **DrvUpgradePrinter** ](https://msdn.microsoft.com/library/windows/hardware/ff548648)関数を設定する必要があります、 **pPrintProcessor**のメンバープリンター\_情報\_新しいプリント プロセッサの名前に 2 つの構造体。 この後、この関数を呼び出す**SetPrinter**プリンターの設定を更新します。 スプーラ呼び出し、 **DrvUpgradePrinter**各プリンターでは、そのドライバーを使用しても、すべてのプリンターが必要なプリント プロセッサを使用することにより、1 回の関数。 次のコード例では、これらの点を示します。

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

 

 




