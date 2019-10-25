---
title: キュー固有ファイルのダウンロード
description: キュー固有ファイルのダウンロード
ms.assetid: b6aad46a-2934-461a-ad11-6ad699687fc1
keywords:
- キュー固有のプリンターファイルをダウンロードしています
- WDK、キュー固有のファイルをポイントして印刷する
- キュー固有ファイル WDK プリンター
- 印刷キューの WDK、ポイント、および印刷
- WDK プリンター、ポイント、および印刷をキューに置いています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bb235322a128a1ab66a7623eb13c8494554e952
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837723"
---
# <a name="downloading-queue-specific-files"></a>キュー固有ファイルのダウンロード





ユーザーがクライアントシステムからプリントサーバーにプリンター接続を作成することにした場合、インストールアプリケーションによって、「[プリンターインストール中のサポートポイントと印刷](supporting-point-and-print-during-printer-installations.md)」で説明されているレジストリエントリが作成されている場合、次のイベントが発生します。可能性

1.  ユーザーアプリケーションは**Addprinterconnection**接続を呼び出します。これについては、Microsoft Windows SDK のドキュメントを参照してください。

2.  クライアントのリモート印刷プロバイダー (Win32spl.dll) は、サーバーへの接続を作成します。

3.  サーバーのスプーラでは、ドライバーファイルがクライアントに送信されます。

4.  クライアントの Win32spl.dll は、サーバー上で enumprinter Key および enumprinter Dataex を呼び出して、プリンターのレジストリエントリをコピーします。

5.  サーバーのスプーラが Enumprinter Dataex の処理中にレジストリ値を列挙すると、次の操作が実行されます。これは、 **copyfiles\\ICM**など、プリンターの**copyfiles**キーのサブキーが検出されるたびに実行されます。
    -   指定されている場合は[ポイントアンドプリント DLL](point-and-print-dlls.md)を読み込み、 [**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths)関数を呼び出します。これにより、ソースパスまたはターゲットパスを変更できます。
    -   **GenerateCopyFilePaths**によって返されたソースとターゲットのパスに基づいて**SourceDir**キーと**TargetDir**キーを作成し、それらを enumプリンター dataex データとしてクライアントスプーラに返します。 (これらのキーはサーバーに実際には存在しません)。

6.  クライアントの Win32spl.dll は、enumprinter Data および enumprinter Dataex 呼び出しへの応答として受信したプリンターキーをキャッシュします。

7.  **Copyfiles\\ICM**など、プリンターの**copyfiles**キーの各サブキーについて、クライアントの win32spl.dll は次の操作を実行します。
    -   ローカルポイントと印刷 DLL が提供されている場合は、それを読み込み、その**GenerateCopyFilePaths**関数を呼び出します。これにより、ソースパスと宛先パスを変更できます。 (入力は、サーバーから受信した**SourceDir**キーと**TargetDir**キーです)。
    -   **ファイル**キーに関連付けられているすべてのファイルをサーバーからダウンロードします。
    -   ポイントと印刷ファイルがダウンロードされたことを示すイベントをログに記録します。
    -   DLL が提供されている場合は、ポイントアンドプリント DLL の[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)関数を呼び出し、COPYFILE\_イベント\_ファイル\_CHANGED イベントを指定します。

8.  クライアントスプーラは、プリンタ\_イベント\_キャッシュ\_更新イベントを指定して、ドライバの[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)関数を呼び出します。

9.  クライアントスプーラは、ドライバの[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)関数を再度呼び出し、プリンタ\_イベント\_\_接続イベントを追加します。

10. ポイントアンドプリント DLL が指定されている場合、クライアントスプーラは COPYFILE\_イベントを指定して[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)関数を呼び出し、\_プリンタ\_接続イベント\_追加します。

### <a name="connection-example"></a>接続の例

例として、インストールアプリケーションで、インストールの例で説明されているサーバーレジストリエントリが定義されているとします。 また、サーバーに NTPRINT.INF という名前を付け、クライアントに MyClient という名前を付けているとします。

NTPRINT.INF で、HpColor という名前の印刷キューに接続するために、MyClient のユーザーアプリケーションは次のように**Addprinterconnection**接続を呼び出します。

```cpp
AddPrinterConnection("\\NTPRINT\HpColor")
```

サーバーでは、スプーラは Mscms を読み込み、次のように[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths)を呼び出します。

```cpp
GenerateCopyFilePaths(
    "HpColor",
    "Color",
    &SplclientInfo1,
    1,
    \\NTPRINT\PRINT$\Color,
    &dwSourceDirSize,
    "Color",
    &dwDestDirSize,
    COPYFILE_FLAG_SERVER_SPOOLER)
```

Microsoft ICM の Mscms モジュールは、ソースまたはターゲットのパスを変更しないので、エラー\_成功します。

サーバースプーラは、MyClient に次のキーを返します。

```cpp
SourceDir: \\NTPRINT\PRINT$\Color
TargetDir: "Color"
```

クライアントでは、 **TargetDir**の値は C:\\Winnt\\System32\\Spool\\Drivers\\Color に展開されます。

MyClient のスプーラは、次の操作を実行します。

-   Mscms をダウンロードし、次のように[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths)を呼び出します。

    ```cpp
    GenerateCopyFilePaths(
        "\\NTPRINT\HpColor",
        "Color",
        &SplclientInfo1,
        1,
        \\NTPRINT\PRINT$\Color,
        &dwSourceDirSize,
        "C:\Winnt\System32\Spool\Drivers\Color",
        &dwDestDirSize,
        COPYFILE_FLAG_CLIENT_SPOOLER)
    ```

    Microsoft ICM の Mscms モジュールは、ソースまたはターゲットのパスを変更しないので、エラー\_成功します。

-   Hpclrlsr をダウンロードします。 icm は C:\\Winnt\\System32\\Spool\\Drivers\\Color.

-   ポイントと印刷ファイルがダウンロードされたことを示すイベントをログに記録します。

-   COPYFILE\_イベント\_ファイル\_CHANGED イベントを指定して、Mscms 内の[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)関数を呼び出します。

-   プリンタ\_イベント\_キャッシュ\_更新イベントを指定して、プリンタドライバの[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)関数を呼び出します。

-   プリンタードライバーの[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)関数を再度呼び出し、\_接続イベント\_追加して、プリンター\_イベントを指定します。

-   Mscms の[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)関数を呼び出します。 COPYFILE\_\_イベントを指定して\_プリンター\_接続イベントを追加します。

 

 




